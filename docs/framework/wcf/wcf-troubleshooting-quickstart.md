---
title: WCF トラブルシューティング クイックスタート
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], troubleshooting
- Windows Communication Foundation [WCF], troubleshooting
ms.assetid: a9ea7a53-f31a-46eb-806e-898e465a4992
ms.openlocfilehash: f85d37fde19767d7fd1e3002776b4816666cc7e8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183052"
---
# <a name="wcf-troubleshooting-quickstart"></a>WCF トラブルシューティング クイックスタート
このトピックでは、WCF クライアントと WCF サービスの開発時に生じるさまざまな既知の問題の一覧を示します。 発生している問題がこの一覧にない場合は、サービスに対してトレースを構成することをお勧めします。 これにより、トレース ファイル ビューアーで表示し、サービス内で発生することがある例外に関する詳細情報を取得できるトレース ファイルが生成されます。 トレースの構成の詳細については、「 [Configuring Tracing](./diagnostics/tracing/configuring-tracing.md)」を参照してください。 トレース ファイル ビューアーの詳細については、「 [Service Trace Viewer Tool (SvcTraceViewer.exe)](service-trace-viewer-tool-svctraceviewer-exe.md)」を参照してください。  
  
1. [Windows 7 と IIS のインストール後に WCF サービスを参照しようとすると、"HTTP エラー 404.3 - Not Found" というエラー メッセージが表示されます](#bkmk_0)  
  
     HTTP エラー 404.3 - Not Found 拡張構成により、要求しているページは使用できません。 ページがスクリプトの場合は、ハンドラーを追加します。 ファイルをダウンロードする場合は、MIME マップを追加します。 エラーの詳細: InformationModule StaticFileModule。  
  
2. [クライアントが最初の要求の後しばらくアイドル状態にある場合、2 番目の要求で MessageSecurityException を受け取ることがあります。どうしたんですか。](#BKMK_q1)  
  
3. [約 10 人のクライアントがやり取りした後、新しいクライアントを拒否するサービスが開始されます。どうしたんですか。](#BKMK_q2)  
  
4. [WCF アプリケーションの構成ファイル以外の場所からサービス構成を読み込むことはできますか。](#BKMK_q3)  
  
5. [サービスとクライアントは素晴らしい仕事をしていますが、クライアントが別のコンピュータにあるときに動作させることはできませんか?どうしたんですか。](#BKMK_q4)  
  
6. [型が例外である場合に\<> FaultException 例外をスローすると、汎用型ではなく、クライアントで常に一般的な FaultException 型が表示されます。どうしたんですか。](#BKMK_q5)  
  
7. [一方向および要求応答操作は、応答にデータが含まれなかった場合にほぼ同じ速度で戻るようです。どうしたんですか。](#BKMK_q6)  
  
8. [私はサービスでX.509証明書を使用しており、System.Security.Cryptography.CryptographicExceptionを取得します。どうしたんですか。](#BKMK_q77)  
  
9. [操作の最初のパラメーターを大文字から小文字に変更しました。今、私のクライアントは例外をスローします。どうしたんですか。](#BKMK_q88)  
  
10. [私はトレースツールの1つを使用していて、エンドポイントNotFoundExceptionを取得します。どうしたんですか。](#BKMK_q99)  
  
11. [WCF SOAP アプリケーションから WCF Web HTTP アプリケーションを呼び出すと、サービスから "405 メソッドは許可されていません" というエラーが返されます](#BK_MK99)  
  
 [ベースアドレスとは何ですか?エンドポイント アドレスとの関係を教えてください。](#BKMK_q10)  
  
<a name="bkmk_0"></a>
## <a name="after-installing-windows-7-and-iis-when-i-attempt-to-browse-to-a-wcf-service-i-get-the-following-error-message-http-error-4043--not-found"></a>Windows 7 と IIS のインストール後に WCF サービスを参照しようとすると、"HTTP エラー 404.3 - Not Found" というエラー メッセージが表示されます  
 エラー メッセージの全文は次のとおりです。  
  
 HTTP エラー 404.3 - Not Found 拡張構成により、要求しているページは使用できません。 ページがスクリプトの場合は、ハンドラーを追加します。 ファイルをダウンロードする場合は、MIME マップを追加します。 エラーの詳細: InformationModule StaticFileModule。  
  
 このエラー メッセージは、コントロール パネルで [Windows 通信財団の HTTP ライセンス認証] が明示的に設定されていない場合に発生します。 これをコントロール パネルに移動するには、ウィンドウの左下隅にある [プログラム] をクリックします。 [Windows の機能の有効化または無効化] をクリックします。 [Microsoft .NET Framework 3.5.1] を展開し、[Windows Communication Foundation HTTP Activation] をクリックします。  
  
<a name="BKMK_q1"></a>
## <a name="sometimes-i-receive-a-messagesecurityexception-on-the-second-request-if-my-client-is-idle-for-a-while-after-the-first-request-what-is-happening"></a>最初の要求の後でクライアントがしばらくアイドル状態になった場合、2 番目の要求で MessageSecurityException を受け取ることがあります。 状況  
 2 番目の要求は、主に次の 2 つの理由から失敗する可能性があります。(1) セッションがタイムアウトした。(2) サービスをホストしている Web サーバーがリサイクルされている。 最初のケースでは、セッションはサービスがタイムアウトするまで有効です。サービスのバインディング (<xref:System.ServiceModel.Channels.Binding.ReceiveTimeout%2A>) で指定された時間内に、サービスがクライアントからの要求を受信しない場合、サービスはセキュリティ セッションを終了します。 それ以降のクライアント メッセージでは、 <xref:System.ServiceModel.Security.MessageSecurityException>が発生します。 クライアントは、セキュリティで保護されたセッションをサービスとの間に再度確立して、後続のメッセージを送信するか、ステートフルなセキュリティ コンテキスト トークンを使用する必要があります。 また、ステートフルなセキュリティ コンテキスト トークンによって、セキュリティで保護されたセッションは、再利用される Web サーバーで存続することができます。 セキュリティで保護されたセッションでステートフル セキュリティ コンテキスト トークンを使用する方法の詳細については、「[方法 : セキュリティで保護されたセッションのセキュリティ コンテキスト トークンを作成する](./feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)」を参照してください。 また、セキュリティで保護されたセッションは無効にできます。 [ \<wsHttpBinding>](../configure-apps/file-schema/wcf/wshttpbinding.md)バインドを使用する場合は、セキュリティ`establishSecurityContext`で保護`false`されたセッションを無効にするプロパティを設定できます。 その他のバインディングでセキュリティで保護されたセッションを無効にするには、カスタム バインディングを作成する必要があります。 カスタム バインディングの作成の詳細については、「 [How to: Create a Custom Binding Using the SecurityBindingElement](./feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)」を参照してください。 このオプションを適用する前に、アプリケーションのセキュリティ要件を確認する必要があります。  
  
<a name="BKMK_q2"></a>
## <a name="my-service-starts-to-reject-new-clients-after-about-10-clients-are-interacting-with-it-what-is-happening"></a>サービスと対話しているクライアントの数が約 10 個になると、サービスが新しいクライアントを拒否し始めます。 状況  
 既定では、サービスは、10 個の同時セッションだけをサポートできます。 したがって、サービス バインディングでセッションを使用する場合、サービスは 10 個に到達するまで新しいクライアント接続を受け入れますが、その数に到達した後は、現在実行中のセッションの 1 つが終了するまで新しいクライアント接続を拒否します。 いくつかの方法で、より多くのクライアントをサポートできます。 サービスにセッションが必要ない場合、セッションの多いバインディングを使用しないでください (詳細については、「[セッションの使用](using-sessions.md)」を参照してください)。もう 1 つの方法は、<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A>プロパティの値を自分の状況に応じた数値に変更することで、セッションの制限を増やします。  
  
<a name="BKMK_q3"></a>
## <a name="can-i-load-my-service-configuration-from-somewhere-other-than-the-wcf-applications-configuration-file"></a>WCF アプリケーションの構成ファイル以外の場所からサービス構成を読み込むことはできますか。  
 できます。ただし、 <xref:System.ServiceModel.ServiceHost> メソッドをオーバーライドするカスタムの <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> クラスを作成する必要があります。 そのメソッドでは、ベースを呼び出して最初に構成を読み込むことができますが (標準の構成情報も読み込む場合)、構成読み込みシステム全体を置き換えることもできます。 アプリケーション構成ファイルとは異なる構成ファイルから構成をロードする場合は、自分で構成ファイルを解析し、構成をロードする必要があります。  
  
 <xref:System.ServiceModel.ServiceHostBase.ApplyConfiguration%2A> メソッドをオーバーライドし、エンドポイントを直接構成する方法を次のコード例に示します。  
  
```csharp
public class MyServiceHost : ServiceHost  
{  
    public MyServiceHost(Type serviceType, params Uri[] baseAddresses)
      : base(serviceType, baseAddresses)  
    {
        Console.WriteLine("MyServiceHost Constructor");
    }  
  
    protected override void ApplyConfiguration()  
    {  
        string straddress = GetAddress();  
        Uri address = new Uri(straddress);  
        Binding binding = GetBinding();  
        base.AddServiceEndpoint(typeof(IData), binding, address);  
    }  
  
    string GetAddress()  
    {
        return "http://MyMachine:7777/MyEndpointAddress/";
    }  
  
    Binding GetBinding()  
    {  
        WSHttpBinding binding = new WSHttpBinding();  
        binding.Security.Mode = SecurityMode.None;  
        return binding;  
    }  
}  
```  
  
<a name="BKMK_q4"></a>
## <a name="my-service-and-client-work-great-but-i-cant-get-them-to-work-when-the-client-is-on-another-computer-whats-happening"></a>サービスとクライアントの動作に問題はないのですが、クライアントが別のコンピューター上にあるときにサービスとクライアントがうまく動作しません。 どうしてでしょうか。  
 例外によっては、次のようないくつかの問題が存在する可能性があります。  
  
- 場合によっては、クライアントのエンドポイント アドレスを "localhost" ではなくホスト名に変更する必要があります。  
  
- 場合によっては、アプリケーションに対してポートを開く必要があります。 詳細については、SDK サンプルから「 [Firewall Instructions](./samples/firewall-instructions.md) 」を参照してください。  
  
- その他の問題については、サンプルトピック[「Windows コミュニケーション ファウンデーション のサンプルの実行](./samples/running-the-samples.md)」を参照してください。  
  
- クライアントが Windows 資格情報を使用し、例外が <xref:System.ServiceModel.Security.SecurityNegotiationException>の場合、次のように Kerberos を設定します。  
  
    1. クライアントの App.config ファイルのエンドポイント要素に ID 資格情報を追加します。  
  
        ```xml
        <endpoint
          address="http://MyServer:8000/MyService/"
          binding="wsHttpBinding"
          bindingConfiguration="WSHttpBinding_IServiceExample"
          contract="IServiceExample"
          behaviorConfiguration="ClientCredBehavior"
          name="WSHttpBinding_IServiceExample">  
          <identity>  
            <userPrincipalName value="name@corp.contoso.com"/>  
          </identity>  
        </endpoint>  
        ```  
  
    2. System または NetworkService アカウントで自己ホスト型サービスを実行します。 次のコマンドを実行すると、System アカウントでコマンド ウィンドウを作成できます。  
  
        ```console
        at 12:36 /interactive "cmd.exe"  
        ```  
  
    3. 既定でサービス プリンシパル名 (SPN) アカウントを使用するインターネット インフォメーション サービス (IIS) でのサービスをホストします。  
  
    4. SetSPN を使用してドメインに新しい SPN を登録します。 これを行うには、ドメイン管理者である必要があります。  
  
 Kerberos プロトコルの詳細については[、「WCF で使用されるセキュリティの概念](./feature-details/security-concepts-used-in-wcf.md)」および「次の項目を参照してください。  
  
- [Windows 認証エラーのデバッグ](./feature-details/debugging-windows-authentication-errors.md)  
  
- [Http.sys を使用した Kerberos サービス プリンシパル名の登録](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms178119(v=sql.105))  
  
- [Kerberos の説明](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742516(v%3dtechnet.10))  
  
<a name="BKMK_q5"></a>
## <a name="when-i-throw-a-faultexceptionexception-where-the-type-is-an-exception-i-always-receive-a-general-faultexception-type-on-the-client-and-not-the-generic-type-whats-happening"></a>型が例外である場合に\<> FaultException 例外をスローすると、汎用型ではなく、クライアントで常に一般的な FaultException 型が表示されます。 どうしてでしょうか。  
 独自のカスタム エラー データ型を作成し、エラー コントラクトで詳細な型としてその型を宣言することをお勧めします。 その理由は、システム指定の例外型を使用すると、次のような状況が起こるためです。  
  
- サービス指向アプリケーションの長所の 1 つを排除する型依存関係が作成されます。  
  
- 標準的な方法でシリアル化している例外に依存できません。 <xref:System.Security.SecurityException>のような例外はまったくシリアル化できない可能性があります。  
  
- クライアントに内部実装の詳細が公開されます。 詳細については、「[コントラクトおよびサービスでの障害の指定と処理](specifying-and-handling-faults-in-contracts-and-services.md)」を参照してください。  
  
 ただし、アプリケーションをデバッグしている場合、 <xref:System.ServiceModel.Description.ServiceDebugBehavior> クラスを使用することによって例外情報をシリアル化して、その情報をクライアントに返すことができます。  
  
<a name="BKMK_q6"></a>
## <a name="it-seems-like-one-way-and-request-reply-operations-return-at-roughly-the-same-speed-when-the-reply-contains-no-data-whats-happening"></a>応答にデータがない場合、一方向操作と要求/応答操作が戻る速度がほぼ同じになるようです。 どうしてでしょうか。  
 操作を一方向に指定すると、操作コントラクトは入力メッセージを受け入れるだけで、出力メッセージを返しません。 WCF では、すべてのクライアント呼び出しは、送信データがワイヤに書き込まれたか、例外がスローされたときに返されます。 一方向操作は同様に動作し、この操作では、サービスが見つからない場合は例外をスローし、サービスがネットワークからのデータの受け入れ準備を完了していない場合はブロックできます。 通常、WCF では、一方向の呼び出しが要求応答よりも迅速にクライアントに返されます。しかし、ネットワーク経由で送信データの送信速度が低下する場合、一方向の操作と要求/応答操作が遅くなります。 詳細については、「[一方向サービス](./feature-details/one-way-services.md)と[WCF クライアントを使用したサービスへのアクセス](./feature-details/accessing-services-using-a-client.md)」を参照してください。  
  
<a name="BKMK_q77"></a>
## <a name="im-using-an-x509-certificate-with-my-service-and-i-get-a-systemsecuritycryptographycryptographicexception-whats-happening"></a>サービスで X.509 証明書を使用していますが、System.Security.Cryptography.CryptographicException を受け取ります。 どうしてでしょうか。  
 この例外は通常、IIS ワーカー プロセスの実行に使用しているユーザー アカウントを変更すると発生します。 たとえば、Windows XP で、Aspnet_wp.exe を実行する既定のユーザー アカウントを ASPNET からカスタム ユーザー アカウントに変更すると、このエラーが表示されることがあります。 秘密キーを使用している場合、そのキーを使用するプロセスには、そのキーを格納しているファイルにアクセスするためのアクセス許可が必要になります。  
  
 この場合、秘密キーを格納しているファイルについて、プロセスのアカウントに読み取りアクセス権を与える必要があります。 たとえば、IIS ワーカー プロセスを Bob というアカウントで実行している場合、秘密キーを格納しているファイルへの読み取りアクセス権を Bob に与える必要があります。  
  
 特定の X.509 証明書の秘密キーを含むファイルへの正しいユーザー アカウント アクセスを付与する方法の詳細については、「[方法: X.509 証明書を WCF からアクセス可能にする](./feature-details/how-to-make-x-509-certificates-accessible-to-wcf.md)」を参照してください。  
  
<a name="BKMK_q88"></a>
## <a name="i-changed-the-first-parameter-of-an-operation-from-uppercase-to-lowercase-now-my-client-throws-an-exception-whats-happening"></a>操作の最初のパラメーターを大文字から小文字に変更したら、クライアントが例外をスローするようになりました。 どうしてでしょうか。  
 操作シグネチャのパラメーター名の値はコントラクトの一部であり、大文字と小文字が区別されます。 ローカル パラメーター名と、クライアント アプリケーションの操作を記述するメタデータを区別する必要がある場合は、 <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType> 属性を使用します。  
  
<a name="BKMK_q99"></a>
## <a name="im-using-one-of-my-tracing-tools-and-i-get-an-endpointnotfoundexception-whats-happening"></a>トレース ツールの 1 つを使用していますが、EndpointNotFoundException を受け取りました。 どうしてでしょうか。  
 システム提供の WCF トレース メカニズムではないトレース ツールを使用していて、アドレス フィルターの<xref:System.ServiceModel.EndpointNotFoundException>不一致があったことを示す を受け取る場合は、<xref:System.ServiceModel.Description.ClientViaBehavior>クラスを使用してトレース ユーティリティにメッセージを送信し、ユーティリティでサービス アドレスにそれらのメッセージをリダイレクトする必要があります。 <xref:System.ServiceModel.Description.ClientViaBehavior> クラスは、 `Via` アドレス指定ヘッダーを変更して、 `To` アドレス指定ヘッダーで示されている最終受信者とは別に、次のネットワーク アドレスを指定します。 ただし、このとき、エンドポイント アドレスは `To` 値の設定に使用されるので変更しないでください。  
  
 次のコード例は、クライアント構成ファイルの例を示しています。  
  
```xml
<endpoint
  address="http://localhost:8000/MyServer/"  
  binding="wsHttpBinding"  
  bindingConfiguration="WSHttpBinding_IMyContract"  
  behaviorConfiguration="MyClient"
  contract="IMyContract"
  name="WSHttpBinding_IMyContract">  
</endpoint>  
<behaviors>  
  <endpointBehaviors>  
    <behavior name="MyClient">  
      <clientVia viaUri="http://localhost:8001/MyServer/"/>  
    </behavior>  
  </endpointBehaviors>  
</behaviors>  
```  
  
<a name="BKMK_q10"></a>
## <a name="what-is-the-base-address-how-does-it-relate-to-an-endpoint-address"></a>ベース アドレスについて教えてください。 エンドポイント アドレスとどのように関連していますか。  
 ベース アドレスとは、 <xref:System.ServiceModel.ServiceHost> クラスのルート アドレスです。 既定では、 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> クラスをサービス構成に追加する場合、ホストが発行するすべてのエンドポイントの Web サービス記述言語 (WSDL) は、HTTP ベース アドレスから取得され、それにメタデータ動作に提供される相対アドレスと "?wsdl" が追加されます。 ASP.NETと IIS に精通している場合、ベース アドレスは仮想ディレクトリと同じです。  
  
## <a name="sharing-a-port-between-a-service-endpoint-and-a-mex-endpoint-using-the-nettcpbinding"></a>NetTcpBinding を使用したサービス エンドポイントと MEX エンドポイント間でのポートの共有  
 サービスのベース アドレスとして net.tcp://MyServer:8080/MyService を指定して次のエンドポイントを追加します。  
  
```xml  
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
 次の構成スニペットに示すように、NetTcpBinding 設定の 1 つを変更するとします。  
  
```xml  
<bindings>  
  <netTcpBinding>  
    <binding closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" transactionFlow="false" transferMode="Buffered" transactionProtocol="OleTransactions" hostNameComparisonMode="StrongWildcard" listenBacklog="10" maxBufferPoolSize="524288" maxBufferSize="65536" maxConnections="11" maxReceivedMessageSize="65536">  
      <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384" maxBytesPerRead="4096" maxNameTableCharCount="16384"/>  
      <reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false"/>  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" protectionLevel="EncryptAndSign"/>  
      </security>  
    </binding>  
  </netTcpBinding>  
</bindings>  
```  
  
 "ハンドルされない例外: System.ServiceModel.AddressAlreadyInUseException: IP エンドポイント 0.0.0.0:9000 には既にリスナーがあります。" というエラーが表示されます。このエラーは、次の構成スニペットに示すように、ポートが異なる完全修飾 URL を MEX エンドポイントに対して指定することで回避できます。  
  
```xml
<services>  
  <service name="Microsoft.Samples.NetTcp.CalculatorService">  
    <endpoint address="calcsvc" binding ="netTcpBinding" contract="Microsoft.Samples.NetTcp.ICalculator"/>  
    <endpoint address="net.tcp://localhost:9001/servicemodelsamples/mex" binding="mexTcpBinding" contract="IMetadataExchange" />  
  </service>  
</services>  
```  
  
<a name="BK_MK99"></a>
## <a name="when-calling-a-wcf-web-http-application-from-a-wcf-soap-application-the-service-returns-the-following-error-405-method-not-allowed"></a>WCF SOAP アプリケーションから WCF Web HTTP アプリケーションを呼び出すと、サービスから "405 メソッドは許可されていません" というエラーが返されます  
 WCF <xref:System.ServiceModel.WebHttpBinding> Web HTTP アプリケーション ( および<xref:System.ServiceModel.Description.WebHttpBehavior>を使用するサービス ) を WCF サービス``Unhandled Exception: System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: The remote server returned an unexpected response: (405) Method Not Allowed.``から呼び出すと、次の例外<xref:System.ServiceModel.OperationContext><xref:System.ServiceModel.OperationContext>が生成されることがあります。 この問題を解決するには、WCF <xref:System.ServiceModel.OperationContextScope> Web HTTP サービス操作内で を作成します。 次に例を示します。  
  
```csharp
public string Echo(string input)  
{  
    using (new OperationContextScope(this.InnerChannel))  
    {  
        return base.Channel.Echo(input);  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [Windows 認証エラーのデバッグ](./feature-details/debugging-windows-authentication-errors.md)
