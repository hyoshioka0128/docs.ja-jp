---
title: 動作を使用したランタイムの構成と拡張
description: WCF アプリで動作インターフェイスを実装し、プログラムまたは構成ファイルでサービスの説明またはエンドポイントに追加する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- attaching extensions using behaviors [WCF]
ms.assetid: 149b99b6-6eb6-4f45-be22-c967279677d9
ms.openlocfilehash: fc297f593b744d69cb09a33be6816fb646f88b67
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247586"
---
# <a name="configuring-and-extending-the-runtime-with-behaviors"></a>動作を使用したランタイムの構成と拡張
動作を使用すると、既定の動作を変更したり、サービス構成を検査および検証するカスタム拡張機能を追加したり、Windows Communication Foundation (WCF) クライアントおよびサービスアプリケーションで実行時の動作を変更したりすることができます。 ここでは、動作インターフェイスとその実装方法について説明します。また、動作インターフェイスをサービスの説明 (サービス アプリケーションの場合) またはエンドポイント (クライアント アプリケーションの場合) にプログラムによって追加する方法と、構成ファイル内で追加する方法についても説明します。 システム指定の動作の使用方法の詳細については、「[サービスの実行時の動作の指定](../specifying-service-run-time-behavior.md)」および「クライアントの[実行時の動作の指定](../specifying-client-run-time-behavior.md)」を参照してください。  
  
## <a name="behaviors"></a>ビヘイビアー  
 動作の種類は、サービスまたはサービスエンドポイント記述オブジェクト (それぞれサービスまたはクライアント上) に追加されます。これらのオブジェクトを Windows Communication Foundation (WCF) で使用して、WCF サービスまたは WCF クライアントを実行するランタイムを作成します。 ランタイムの構築プロセスでこれらの動作を呼び出すと、コントラクト、バインディング、およびアドレスによって構築されたランタイムを変更するランタイム プロパティやランタイム メソッドにアクセスできます。  
  
### <a name="behavior-methods"></a>動作メソッド  
 すべての動作で、`AddBindingParameters` メソッド、`ApplyDispatchBehavior` メソッド、`Validate` メソッド、および `ApplyClientBehavior` メソッドを使用できます。ただし、<xref:System.ServiceModel.Description.IServiceBehavior> には、例外が 1 つあります。`ApplyClientBehavior` はクライアントで実行できないため、このメソッドを実装していません。  
  
- カスタム オブジェクトを変更したり、ランタイム構築時に使用するためにカスタム バインディングがアクセスできるコレクションにカスタム オブジェクトを追加したりするには、`AddBindingParameters` メソッドを使用します。 たとえば、これによって、チャネルを構築する方法に影響するが、チャネル開発者には知られていない保護要件を指定します。  
  
- 説明ツリーと対応するランタイム オブジェクトを検査し、特定の基準セットに従っていることを確認するには、`Validate` メソッドを使用します。  
  
- 説明ツリーを検査し、サービスまたはクライアントの特定のスコープのランタイムを変更するには、`ApplyDispatchBehavior` メソッドと `ApplyClientBehavior` メソッドを使用します。 また、拡張オブジェクトを挿入することもできます。  
  
    > [!NOTE]
    > これらのメソッドでは説明ツリーが提供されますが、説明ツリーは検査にのみ使用します。 説明ツリーを変更すると、動作は未定義の状態になります。  
  
 変更できるプロパティと実装できるカスタマイズ インターフェイスには、サービスおよびクライアントのランタイム クラスからアクセスできます。 サービス型は、<xref:System.ServiceModel.Dispatcher.DispatchRuntime> クラスと <xref:System.ServiceModel.Dispatcher.DispatchOperation> クラスです。 クライアント型は、<xref:System.ServiceModel.Dispatcher.ClientRuntime> クラスと <xref:System.ServiceModel.Dispatcher.ClientOperation> クラスです。 <xref:System.ServiceModel.Dispatcher.ClientRuntime> クラスと <xref:System.ServiceModel.Dispatcher.DispatchRuntime> クラスは、それぞれクライアント全体またはサービス全体のランタイム プロパティと拡張コレクションにアクセスするための拡張エントリ ポイントです。 同様に、<xref:System.ServiceModel.Dispatcher.ClientOperation> クラスと <xref:System.ServiceModel.Dispatcher.DispatchOperation> クラスは、それぞれクライアント操作またはサービス操作のランタイム プロパティと拡張コレクションを公開します。 ただし、必要に応じて、操作ランタイム オブジェクトからより広いスコープのランタイム オブジェクトにアクセスできます。また、逆の場合も同様です。  
  
> [!NOTE]
> クライアントの実行動作を変更するために使用できるランタイムプロパティと拡張機能の種類の詳細については、「[クライアントの拡張](extending-clients.md)」を参照してください。 サービスディスパッチャーの実行動作を変更するために使用できるランタイムプロパティと拡張型の詳細については、「[ディスパッチャーの拡張](extending-dispatchers.md)」を参照してください。  
  
 ほとんどの WCF ユーザーは、ランタイムと直接やり取りしません。代わりに、構成ファイルのクラスまたは動作のエンドポイント、コントラクト、バインディング、アドレス、動作属性などの主要なプログラミングモデル構造を使用します。 これらのコンストラクトは、説明ツリーを*構成します*。これは、説明ツリーによって記述されたサービスまたはクライアントをサポートするランタイムを構築するための完全な仕様です。  
  
 WCF には、次の4種類の動作があります。  
  
- サービスの動作 (<xref:System.ServiceModel.Description.IServiceBehavior> 型) : <xref:System.ServiceModel.ServiceHostBase> を含むサービス ランタイム全体のカスタマイズを実現します。  
  
- エンドポイントの動作 (<xref:System.ServiceModel.Description.IEndpointBehavior> 型) : サービス エンドポイントと、関連する <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> オブジェクトのカスタマイズを実現します。  
  
- コントラクトの動作 (<xref:System.ServiceModel.Description.IContractBehavior> 型) : <xref:System.ServiceModel.Dispatcher.ClientRuntime> クラス (クライアント アプリケーションの場合) と、<xref:System.ServiceModel.Dispatcher.DispatchRuntime> クラス (サービス アプリケーションの場合) のカスタマイズを実現します。  
  
- 操作の動作 (<xref:System.ServiceModel.Description.IOperationBehavior> 型) : <xref:System.ServiceModel.Dispatcher.ClientOperation> クラス (クライアントの場合) と、<xref:System.ServiceModel.Dispatcher.DispatchOperation> クラス (サービスの場合) のカスタマイズを実現します。  
  
 カスタム属性を実装するか、アプリケーション構成ファイルを使用することにより、これらの動作をさまざまな説明オブジェクトに追加できます。また、適切な説明オブジェクトの動作コレクションに直接追加することもできます。 ただし、<xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> または <xref:System.ServiceModel.ServiceHost> で <xref:System.ServiceModel.ChannelFactory%601> を呼び出す前に、サービス説明オブジェクトまたはサービス エンドポイント説明オブジェクトに追加する必要があります。  
  
### <a name="behavior-scopes"></a>動作のスコープ  
 4 種類の動作があり、それぞれランタイム アクセスの特定のスコープに対応しています。  
  
#### <a name="service-behaviors"></a>サービスの動作  
 <xref:System.ServiceModel.Description.IServiceBehavior> を実装するサービスの動作は、サービス ランタイム全体を変更する主要機構です。 サービスの動作をサービスに追加する場合、3 つの方法があります。  
  
1. サービス クラスの属性を使用する方法。  <xref:System.ServiceModel.ServiceHost> を構築すると、<xref:System.ServiceModel.ServiceHost> 実装は、リフレクションを使用してそのサービス型の属性セットを検出します。 これらの属性のいずれかが <xref:System.ServiceModel.Description.IServiceBehavior> の実装である場合、<xref:System.ServiceModel.Description.ServiceDescription> の動作コレクションに追加されます。 これにより、これらの動作はサービス ランタイムの構築に参加できます。  
  
2. プログラムによって、<xref:System.ServiceModel.Description.ServiceDescription> の動作コレクションに動作を追加する方法。 これを行うには、次のコード行を使用します。  
  
    ```csharp
    ServiceHost host = new ServiceHost(/* Parameters */);  
    host.Description.Behaviors.Add(/* Service Behavior */);  
    ```  
  
3. 構成を拡張するカスタムの <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> を実装する方法。 これにより、アプリケーション構成ファイルからサービスの動作を使用できるようになります。  
  
 WCF のサービス動作の例としては、 <xref:System.ServiceModel.ServiceBehaviorAttribute> 属性、、 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> および動作があり <xref:System.ServiceModel.Description.ServiceMetadataBehavior> ます。  
  
#### <a name="contract-behaviors"></a>コントラクトの動作  
 <xref:System.ServiceModel.Description.IContractBehavior> インターフェイスを実装するコントラクトの動作は、コントラクト全体にわたり、クライアント ランタイムとサービス ランタイムを拡張する際に使用します。  
  
 コントラクトの動作をコントラクトに追加する場合、2 つの方法があります。  1 つは、コントラクト インターフェイスで使用するカスタム属性を作成する方法です。 コントラクトインターフェイスがまたはに渡されると <xref:System.ServiceModel.ServiceHost> <xref:System.ServiceModel.ChannelFactory%601> 、WCF はインターフェイスの属性を調べます。 属性のいずれかが <xref:System.ServiceModel.Description.IContractBehavior> の実装である場合、そのインターフェイス用に作成された <xref:System.ServiceModel.Description.ContractDescription?displayProperty=nameWithType> の動作コレクションに追加されます。  
  
 カスタム コントラクトの動作属性に <xref:System.ServiceModel.Description.IContractBehaviorAttribute?displayProperty=nameWithType> を実装することもできます。 この場合、適用先に応じて動作は次のようになります。  
  
 •コントラクト インターフェイスに適用した場合。 この場合、動作は任意のエンドポイントでその型のすべてのコントラクトに適用され、WCF はプロパティの値を無視し <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A?displayProperty=nameWithType> ます。  
  
 •サービス クラスに適用した場合。 この場合、動作はコントラクトが <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A> プロパティの値であるエンドポイントにのみ適用されます。  
  
 •コールバック クラスに適用した場合。 この場合、動作は双方向クライアントのエンドポイントに適用され、WCF はプロパティの値を無視し <xref:System.ServiceModel.Description.IContractBehaviorAttribute.TargetContract%2A> ます。  
  
 2 番目の方法として、<xref:System.ServiceModel.Description.ContractDescription> の動作コレクションに動作を追加する方法があります。  
  
 WCF のコントラクト動作の例には、属性が含ま <xref:System.ServiceModel.DeliveryRequirementsAttribute?displayProperty=nameWithType> れています。 詳細および例については、リファレンス トピックを参照してください。  
  
#### <a name="endpoint-behaviors"></a>エンドポイントの動作  
 <xref:System.ServiceModel.Description.IEndpointBehavior> を実装するエンドポイントの動作は、特定のエンドポイントのサービス ランタイムまたはクライアント ランタイム全体を変更する主要機構です。  
  
 エンドポイントの動作をサービスに追加する場合、2 つの方法があります。  
  
1. <xref:System.ServiceModel.Description.ServiceEndpoint.Behaviors%2A> プロパティに動作を追加する方法。  
  
2. 構成を拡張するカスタムの <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> を実装する方法。  
  
 詳細および例については、リファレンス トピックを参照してください。  
  
#### <a name="operation-behaviors"></a>操作の動作  
 <xref:System.ServiceModel.Description.IOperationBehavior> インターフェイスを実装する操作の動作は、各操作のクライアント ランタイムとサービス ランタイムを拡張する際に使用します。  
  
 操作の動作を操作に追加する場合、2 つの方法があります。 1 つは、操作をモデル化するメソッドで使用するカスタム属性を作成する方法です。 操作がまたはのいずれかに追加されると <xref:System.ServiceModel.ServiceHost> <xref:System.ServiceModel.ChannelFactory> 、WCF は、 <xref:System.ServiceModel.Description.IOperationBehavior> <xref:System.ServiceModel.Description.OperationDescription> その操作用に作成されたの動作コレクションに属性を追加します。  
  
 2 番目の機構は、構成された <xref:System.ServiceModel.Description.OperationDescription> の動作コレクションに動作を直接追加します。  
  
 WCF での操作の動作の例として、およびがあり <xref:System.ServiceModel.OperationBehaviorAttribute> <xref:System.ServiceModel.TransactionFlowAttribute> ます。  
  
 詳細および例については、リファレンス トピックを参照してください。  
  
### <a name="using-configuration-to-create-behaviors"></a>構成を使用した動作の作成  
 サービス、エンドポイント、およびコントラクトの動作は、コードまたは属性を使用して指定するように設計できます。アプリケーション構成ファイルまたは Web 構成ファイルを使用して構成できるのは、サービスの動作とエンドポイントの動作だけです。 属性を使用して動作を公開した場合、開発者は、実行時に追加、削除、または変更できない動作をコンパイル時に指定できます。 多くの場合、これはサービスの適切な操作のために常に必要となる動作に適しています (<xref:System.ServiceModel.ServiceBehaviorAttribute?displayProperty=nameWithType> 属性に対するトランザクション関連のパラメーターなど)。 構成を使用して動作を公開すると、開発者はサービス展開者に動作の仕様と構成を委ねることができます。 これは、動作がオプション コンポーネント、または他の展開固有の構成 (サービスまたはサービスの特定の承認構成についてメタデータを公開するかどうかなど) である場合に適しています。  
  
> [!NOTE]
> 企業のアプリケーション ポリシーを machine.config 構成ファイルに挿入し、これらの項目をロックダウンすることで、ポリシーを適用する構成をサポートする動作を使用することもできます。 説明と例については、「[方法: 企業内のエンドポイントをロックダウンする](how-to-lock-down-endpoints-in-the-enterprise.md)」を参照してください。  
  
 構成を使用して動作を公開するには、開発者は <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> の派生クラスを作成し、その拡張を構成に登録する必要があります。  
  
 <xref:System.ServiceModel.Description.IEndpointBehavior> で <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> を実装する方法を次のコード例に示します。  
  
```csharp
// BehaviorExtensionElement members  
public override Type BehaviorType  
{  
  get { return typeof(EndpointBehaviorMessageInspector); }  
}  
  
protected override object CreateBehavior()  
{  
  return new EndpointBehaviorMessageInspector();  
}  
```  
  
 構成システムでカスタムの <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> を読み込むには、拡張として登録する必要があります。 上記のエンドポイントの動作の構成ファイルを次のコード例に示します。  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service
        name="Microsoft.WCF.Documentation.SampleService"  
        behaviorConfiguration="metadataSupport"  
      >  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8080/ServiceMetadata" />  
          </baseAddresses>  
        </host>  
        <endpoint  
          address="/SampleService"  
          binding="wsHttpBinding"  
          behaviorConfiguration="withMessageInspector"
          contract="Microsoft.WCF.Documentation.ISampleService"  
        />  
        <endpoint  
           address="mex"  
           binding="mexHttpBinding"  
           contract="IMetadataExchange"  
        />  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
      <behavior name="metadataSupport">  
        <serviceMetadata httpGetEnabled="true" httpGetUrl=""/>  
      </behavior>  
      </serviceBehaviors>  
      <endpointBehaviors>  
        <behavior name="withMessageInspector">  
          <endpointMessageInspector />  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <extensions>  
      <behaviorExtensions>  
        <add
          name="endpointMessageInspector"  
          type="Microsoft.WCF.Documentation.EndpointBehaviorMessageInspector, HostApplication, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null"  
        />  
      </behaviorExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
 ここで、 `Microsoft.WCF.Documentation.EndpointBehaviorMessageInspector` は動作拡張機能の種類で、 `HostApplication` はそのクラスがコンパイルされたアセンブリの名前です。  
  
### <a name="evaluation-order"></a>評価順序  
 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> と <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> は、プログラミング モデルと記述からランタイムを構築します。 前述のように、動作は、サービス、エンドポイント、コントラクト、および操作でランタイムの構築プロセスを支援します。  
  
 <xref:System.ServiceModel.ServiceHost> は次の順序で動作を適用します。  
  
1. サービス  
  
2. コントラクト  
  
3. エンドポイント  
  
4. 操作  
  
 動作のどのコレクション内でも、順序が保証されるというわけではありません。  
  
 <xref:System.ServiceModel.ChannelFactory%601> は次の順序で動作を適用します。  
  
1. コントラクト  
  
2. エンドポイント  
  
3. 操作  
  
 この場合も、動作のどのコレクション内でも、順序が保証されるというわけではありません。  
  
### <a name="adding-behaviors-programmatically"></a>プログラムによる動作の追加  
 <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=nameWithType> の <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A?displayProperty=nameWithType> メソッドの後で、サービス アプリケーションの <xref:System.ServiceModel.ServiceHostBase?displayProperty=nameWithType> の各プロパティを変更しないでください。 このメソッドの後で変更すると、<xref:System.ServiceModel.ServiceHostBase.Credentials%2A?displayProperty=nameWithType> および `AddServiceEndpoint` の <xref:System.ServiceModel.ServiceHostBase> プロパティや <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> メソッドなどの一部のメンバーは例外をスローします。 変更を許可するメンバーもありますが、結果は未定義の状態になります。  
  
 同様に、クライアントで、<xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType> の <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> 呼び出しの後で、<xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> 値を変更しないでください。 この呼び出しの後で変更すると、<xref:System.ServiceModel.ChannelFactory.Credentials%2A?displayProperty=nameWithType> プロパティは例外をスローします。その他のクライアント記述値は、エラーを発生させずに変更できます。 ただし、結果は未定義の状態になります。  
  
 サービスとクライアントのどちらの場合も、<xref:System.ServiceModel.Channels.CommunicationObject.Open%2A?displayProperty=nameWithType> の呼び出しの前に記述を変更することをお勧めします。  
  
### <a name="inheritance-rules-for-behavior-attributes"></a>動作属性の継承ルール  
 4 種類の動作はすべて、属性 (サービスの動作とコントラクトの動作) を使用して設定できます。 属性はマネージド オブジェクトとメンバーで定義され、マネージド オブジェクトとメンバーは継承をサポートしているため、継承のコンテキストでの動作属性の機能を定義する必要があります。  
  
 大まかに言えば、特定のスコープ (サービス、コントラクト、操作など) については、そのスコープの継承階層内のすべての動作属性が適用されるという継承ルールになります。 同じ種類の 2 つの動作属性がある場合、最も多く派生された種類だけが使用されます。  
  
#### <a name="service-behaviors"></a>サービスの動作  
 サービス クラスの場合、指定のクラスとその親のすべてのサービス動作属性が適用されます。 継承階層の複数の場所に同じ種類の属性が適用されている場合は、最も多く派生された種類が使用されます。  
  
```csharp  
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Multiple)]  
[AspNetCompatibilityRequirementsAttribute(  
    AspNetCompatibilityRequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
public class A { /* … */ }  
  
[ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
public class B : A { /* … */}  
```  
  
 たとえば、上記の例では、最終的にサービス B は、<xref:System.ServiceModel.InstanceContextMode> が <xref:System.ServiceModel.InstanceContextMode.Single>、<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode> が <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed>、<xref:System.ServiceModel.ConcurrencyMode> が <xref:System.ServiceModel.ConcurrencyMode.Single> になります。 <xref:System.ServiceModel.ConcurrencyMode> が <xref:System.ServiceModel.ConcurrencyMode.Single> になるのは、サービス B の <xref:System.ServiceModel.ServiceBehaviorAttribute> 属性の方がサービス A よりも多く派生されているためです。  
  
#### <a name="contract-behaviors"></a>コントラクトの動作  
 コントラクトの場合、指定のインターフェイスとその親のすべてのコントラクト動作属性が適用されます。 継承階層の複数の場所に同じ種類の属性が適用されている場合は、最も多く派生された種類が使用されます。  
  
#### <a name="operation-behaviors"></a>操作の動作  
 指定の操作が既存の抽象操作または仮想操作をオーバーライドしない場合、継承ルールは適用されません。  
  
 操作が既存の操作をオーバーライドする場合は、その操作とその親のすべての操作動作属性が適用されます。  継承階層の複数の場所に同じ種類の属性が適用されている場合は、最も多く派生された種類が使用されます。
