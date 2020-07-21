---
title: 本文別のルーティング
ms.date: 03/30/2017
ms.assetid: 07a6fc3b-c360-42e0-b663-3d0f22cf4502
ms.openlocfilehash: 146baf806f4922f5e3ddd92a762772786e61d443
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594596"
---
# <a name="route-by-body"></a>本文別のルーティング
このサンプルでは、任意の SOAP アクションでメッセージ オブジェクトを受け入れるサービスを実装する方法を示します。 このサンプルは、電卓サービスを実装する[はじめに](getting-started-sample.md)に基づいています。 このサービスは、`Calculate` 要求パラメータを受け入れる 1 つの <xref:System.ServiceModel.Channels.Message> 操作を実装して、<xref:System.ServiceModel.Channels.Message> 応答を返します。  
  
 このサンプルでは、クライアントはコンソール アプリケーション (.exe) で、サービスは IIS によってホストされています。  
  
> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
 このサンプルでは、本文の内容に基づくメッセージ ディスパッチを示します。 組み込みの Windows Communication Foundation (WCF) サービスモデルメッセージのディスパッチメカニズムは、メッセージアクションに基づいています。 ただし既存の多くの Web サービスでは、すべての操作が Action="" で定義されています。 アクション情報に基づいてディスパッチ要求メッセージを保持する WSDL を基準として、サービスを構築することはできません。 このサンプルでは、WSDL に基づくサービス コントラクトを示します (WSDL はこのサンプルに含まれる Service.wsdl 内に格納されています)。 サービスコントラクトは、[はじめに](getting-started-sample.md)で使用されるものと同様に、計算ツールです。 ただし、`[OperationContract]` は、すべての操作に対して `Action=""` を指定します。  
  
```csharp  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples"),
                 XmlSerializerFormat, DispatchByBodyBehavior]  
    public interface ICalculator  
    {  
        [OperationContract(Action="")]  
        double Add(double n1, double n2);  
        [OperationContract(Action = "")]  
        double Subtract(double n1, double n2);  
        [OperationContract(Action = "")]  
        double Multiply(double n1, double n2);  
        [OperationContract(Action = "")]  
        double Divide(double n1, double n2);  
    }  
```  
  
 コントラクトが指定されている場合、サービスはカスタムのディスパッチ動作 `DispatchByBodyBehavior` に対して、複数の操作間でメッセージをディスパッチするように要求します。 このディスパッチ動作は、 `DispatchByBodyElementOperationSelector` カスタム操作セレクターを、それぞれのラッパー要素の QName をキーとする操作名のテーブルを使用して初期化します。 `DispatchByBodyElementOperationSelector` は本文の最初の子の開始タグを参照し、前述のテーブルを使用して操作を選択します。  
  
 クライアントは、 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用して、サービスによってエクスポートされた WSDL から自動生成されたプロキシを使用します。  
  
```console  
svcutil.exe  /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples /uxs http://localhost/servicemodelsamples/service.svc?wsdl /out:generatedProxy.cs  
```  
  
 すべての操作のアクションが空であっても、クライアント コードには影響ありません。ただし、自動生成されたプロキシ内の Action パラメータは例外です。  
  
 クライアント コードは、複数の計算を実行します。 このサンプルを実行すると、操作要求および応答がクライアントのコンソール ウィンドウに表示されます。 クライアントをシャットダウンするには、クライアント ウィンドウで Enter キーを押します。  
  
```console
Add(100, 15.99) = 115.99  
Subtract(145, 76.54) = 68.46  
Multiply(9, 81.25) = 731.25  
Divide(22, 7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。  
  
2. ソリューションをビルドするには、「 [Windows Communication Foundation サンプルのビルド](building-the-samples.md)」の手順に従います。  
  
3. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Interop\RouteByBody`  
