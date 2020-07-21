---
title: カスタム サービス ホスト
ms.date: 03/30/2017
ms.assetid: fe16ff50-7156-4499-9c32-13d8a79dc100
ms.openlocfilehash: 8302c3c829883da954d200526ca641eb4c169f98
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052027"
---
# <a name="custom-service-host"></a>カスタム サービス ホスト
このサンプルでは、<xref:System.ServiceModel.ServiceHost> クラスから派生したカスタムのサービス ホストを使用して、サービスの実行時動作を変更する方法を示します。 この方法は、多数のサービスを共通方式で構成するという方法の代わりに使用でき、再利用可能です。 このサンプルでは、<xref:System.ServiceModel.Activation.ServiceHostFactory> クラスを使用して、カスタムの ServiceHost を、インターネット インフォメーション サービス (IIS) または Windows プロセス アクティブ化サービス (WAS) でホストされる環境で使用する方法も示します。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Hosting\CustomServiceHost`  
  
## <a name="about-the-scenario"></a>シナリオについて
 機密性の高いサービスメタデータが誤って公開されるのを防ぐために、Windows Communication Foundation (WCF) サービスの既定の構成では、メタデータの公開が無効になっています。 この動作は既定ではセキュリティで保護されていますが、サービスのメタデータ公開動作が構成で明示的に有効になっていない限り、サービスの呼び出しに必要なクライアントコードを生成するためにメタデータインポートツール (Svcutil.exe など) を使用することはできません。  
  
 多数のサービスのメタデータ公開を有効にすると、同一の構成要素が各サービスに追加されます。この結果、本質的に同じ構成情報が大量に発生することになります。 各サービスを個別に構成する代わりに、メタデータ公開を有効化する命令型コードを一度だけプログラミングして、そのコードを複数のサービスで再利用するという方法もあります。 この方法を使用するには、<xref:System.ServiceModel.ServiceHost> から派生する新しいクラスを作成し、`ApplyConfiguration`() メソッドをオーバーライドして命令型コードでメタデータ公開動作を追加します。  
  
> [!IMPORTANT]
> このサンプルでは、わかりやすくするために、セキュリティで保護されていないメタデータ公開エンドポイントを作成する方法を示します。 このようなエンドポイントは、匿名の認証されていないコンシューマーが使用できる可能性があり、サービスのメタデータの公開が適切であることを保証するために、このようなエンドポイントをデプロイする前に注意する必要が  
  
## <a name="implementing-a-custom-servicehost"></a>カスタム ServiceHost の実装
 <xref:System.ServiceModel.ServiceHost> クラスは、便利な仮想メソッドを多数公開しています。継承側でこの仮想メソッドをオーバーライドして、サービスの実行時動作を変更することができます。 たとえば、`ApplyConfiguration`() メソッドはサービスの構成情報を構成ストアから読み取り、それに応じてホストの <xref:System.ServiceModel.Description.ServiceDescription> を変更します。 既定の実装では、アプリケーションの構成ファイルから構成を読み取ります。 カスタム実装では、`ApplyConfiguration`() をオーバーライドすれば、命令型コードを使用して <xref:System.ServiceModel.Description.ServiceDescription> にさらに変更を加えることや、既定の構成ストア全体を置き換えることも可能です ( たとえば、アプリケーションの構成ファイルではなく、データベースからサービスのエンドポイント構成を読み取ることができます。  
  
 このサンプルでは、サービスの構成ファイルにこの動作が明示的に追加されていない場合でも、ServiceMetadataBehavior (メタデータの公開を有効にする) を追加するカスタム ServiceHost を作成します。 これを実現するには、から継承して () をオーバーライドする新しいクラスを作成し <xref:System.ServiceModel.ServiceHost> `ApplyConfiguration` ます。  
  
```csharp
class SelfDescribingServiceHost : ServiceHost  
{  
    public SelfDescribingServiceHost(Type serviceType, params Uri[] baseAddresses)  
        : base(serviceType, baseAddresses) { }  
  
    //Overriding ApplyConfiguration() allows us to
    //alter the ServiceDescription prior to opening  
    //the service host.
    protected override void ApplyConfiguration()  
    {  
        //First, we call base.ApplyConfiguration()  
        //to read any configuration that was provided for  
        //the service we're hosting. After this call,  
        //this.Description describes the service  
        //as it was configured.  
        base.ApplyConfiguration();
  
        //(rest of implementation elided for clarity)  
    }  
}  
```  
  
 アプリケーションの構成ファイルで提供されている構成を無視したくないので、() の最初のオーバーライド `ApplyConfiguration` は基本実装を呼び出します。 このメソッドが完了した後で、次の命令型コードを使用して、サービス記述に <xref:System.ServiceModel.Description.ServiceMetadataBehavior> を追加します。  
  
```csharp
ServiceMetadataBehavior mexBehavior = this.Description.Behaviors.Find<ServiceMetadataBehavior>();  
if (mexBehavior == null)  
{  
    mexBehavior = new ServiceMetadataBehavior();  
    this.Description.Behaviors.Add(mexBehavior);  
}  
else  
{  
    //Metadata behavior has already been configured,
    //so we do not have any work to do.  
    return;  
}  
```  
  
 `ApplyConfiguration`() のオーバーライドでの最後の処理は、既定のメタデータ エンドポイントの追加です。 慣例により、サービスホストの BaseAddresses コレクション内の各 URI に対して1つのメタデータエンドポイントが作成されます。  
  
```csharp
//Add a metadata endpoint at each base address  
//using the "/mex" addressing convention  
foreach (Uri baseAddress in this.BaseAddresses)  
{  
    if (baseAddress.Scheme == Uri.UriSchemeHttp)  
    {  
        mexBehavior.HttpGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeHttps)  
    {  
        mexBehavior.HttpsGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpsBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetPipe)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexNamedPipeBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetTcp)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexTcpBinding(),  
                                "mex");  
    }  
}  
```  
  
## <a name="using-a-custom-servicehost-in-self-host"></a>自己ホストでのカスタム ServiceHost の使用  
 カスタム ServiceHost の実装が完成したので、これを使用して任意のサービスにメタデータ公開動作を追加できるようになりました。追加するには、`SelfDescribingServiceHost` のインスタンス内でサービスをホストします。 カスタム ServiceHost を自己ホストのシナリオで使用する方法を次のコードに示します。  
  
```csharp
SelfDescribingServiceHost host =
         new SelfDescribingServiceHost( typeof( Calculator ) );  
host.Open();  
```  
  
 既定のクラスを使用してサービスをホストしていたかのように、カスタムホストは引き続きアプリケーションの構成ファイルからサービスのエンドポイント構成を読み取り <xref:System.ServiceModel.ServiceHost> ます。 ただし、カスタム ホストの内部でメタデータ公開を有効にするというロジックを追加したので、構成の中でメタデータ公開動作を明示的に有効化することは不要になりました。 この方法のメリットがはっきりと現れるのは、開発するアプリケーションに複数のサービスがあり、同じ構成要素を繰り返し記述することなく各サービスでメタデータ公開を有効化できるようにする場合です。  
  
## <a name="using-a-custom-servicehost-in-iis-or-was"></a>IIS または WAS でのカスタム ServiceHost の使用  
 カスタム サービス ホストを自己ホストのシナリオで使用することは簡単です。サービス ホストのインスタンスを作成して開くことは、アプリケーションのコードで行うからです。 ただし、IIS または WAS のホスト環境では、WCF インフラストラクチャは、受信メッセージに応答してサービスのホストを動的にインスタンス化します。 このホスト環境でもカスタム サービス ホストを使用できますが、ServiceHostFactory の形式でコードを追加する必要があります。 次に示すコードは、カスタム <xref:System.ServiceModel.Activation.ServiceHostFactory> のインスタンスを返す、`SelfDescribingServiceHost` の派生クラスの例です。  
  
```csharp
public class SelfDescribingServiceHostFactory : ServiceHostFactory  
{  
    protected override ServiceHost CreateServiceHost(Type serviceType,
     Uri[] baseAddresses)  
    {  
        //All the custom factory does is return a new instance  
        //of our custom host class. The bulk of the custom logic should  
        //live in the custom host (as opposed to the factory)
        //for maximum  
        //reuse value outside of the IIS/WAS hosting environment.  
        return new SelfDescribingServiceHost(serviceType,
                                             baseAddresses);  
    }  
}  
```  
  
 ご覧のように、カスタム ServiceHostFactory の実装は簡単です。 すべてのカスタム ロジックは ServiceHost 実装内部にあり、このファクトリによって派生クラスのインスタンスが返されます。  
  
 サービス実装でカスタムファクトリを使用するには、サービスの .svc ファイルに追加のメタデータを追加する必要があります。  
  
```aspx-csharp
<% @ServiceHost Service="Microsoft.ServiceModel.Samples.CalculatorService"
               Factory="Microsoft.ServiceModel.Samples.SelfDescribingServiceHostFactory"
               language=c# Debug="true" %>
```
  
 ここでは、 `Factory` ディレクティブに追加の属性を追加 `@ServiceHost` し、属性の値としてカスタムファクトリの CLR 型名を渡しました。 IIS または WAS がこのサービスのメッセージを受信すると、WCF ホスティングインフラストラクチャは、まず ServiceHostFactory のインスタンスを作成してから、を呼び出してサービスホスト自体をインスタンス化し `ServiceHostFactory.CreateServiceHost()` ます。  
  
## <a name="running-the-sample"></a>サンプルの実行  
 このサンプルでは、完全に機能するクライアントとサービスの実装を提供していますが、サンプルのポイントは、カスタムホストを使用してサービスの実行時の動作を変更する方法を示しています。次の手順を実行します。  
  
### <a name="observe-the-effect-of-the-custom-host"></a>カスタムホストの効果を確認する
  
1. サービスの Web.config ファイルを開き、サービスのメタデータを明示的に有効にする構成がないことを確認します。  
  
2. サービスの .svc ファイルを開き、 @ServiceHost ディレクティブにカスタム ServiceHostFactory の名前を指定するファクトリ属性が含まれていることを確認します。  
  
### <a name="set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行する
  
1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。

2. ソリューションをビルドするには、「 [Windows Communication Foundation サンプルのビルド](building-the-samples.md)」の手順に従います。

3. ソリューションをビルドした後、Setup.bat を実行して IIS 7.0 で ServiceModelSamples アプリケーションを設定します。 これで、ServiceModelSamples ディレクトリが IIS 7.0 アプリケーションとして表示されます。

4. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。

5. IIS 7.0 アプリケーションを削除するには、 *Cleanup.bat*を実行します。

## <a name="see-also"></a>関連項目

- [方法: IIS で WCF サービスをホストする](../feature-details/how-to-host-a-wcf-service-in-iis.md)
