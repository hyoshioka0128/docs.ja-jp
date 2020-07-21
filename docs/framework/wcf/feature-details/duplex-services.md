---
title: 双方向サービス
description: WCF で双方向サービスコントラクトを作成する方法について説明します。これにより、両方のエンドポイントが、クライアントによって作成されたチャネルを介して相互にメッセージを送信できるようになります。
ms.date: 05/09/2018
dev_langs:
- csharp
- vb
ms.assetid: 396b875a-d203-4ebe-a3a1-6a330d962e95
ms.openlocfilehash: a43bb63a0ccf1a34b79dce755c19f7ed4cb6c16c
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247352"
---
# <a name="duplex-services"></a>双方向サービス

双方向サービス コントラクトは、両方のエンドポイントが互いに独立してメッセージを送信できるメッセージ交換パターンです。 双方向サービスでは、クライアントのエンドポイントにメッセージを返信できるため、イベントのような動作を実現できます。 双方向通信は、クライアントがサービスに接続し、サービスからクライアントにメッセージを返信できるチャネルがサービスに提供されると発生します。 双方向サービスにおけるイベントのような動作は、セッション内でのみ機能することに注意してください。

双方向コントラクトを作成するには、インターフェイスのペアを作成します。 最初のインターフェイスは、クライアントから呼び出すことのできる操作を記述したサービス コントラクト インターフェイスです。 このサービスコントラクトは、プロパティで*コールバックコントラクト*を指定する必要があり <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A?displayProperty=nameWithType> ます。 このコールバック コントラクトが、サービスがクライアント エンドポイントで呼び出すことのできる操作を定義するインターフェイスになります。 双方向コントラクトではセッションは必要ありませんが、システム指定の二重バインディングではセッションを利用します。

双方向コントラクトの例を次に示します。

[!code-csharp[c_DuplexServices#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#0)]
[!code-vb[c_DuplexServices#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#0)]

`CalculatorService` クラスは、プライマリ `ICalculatorDuplex` インターフェイスを実装します。 このサービスは <xref:System.ServiceModel.InstanceContextMode.PerSession> インスタンス モードを使用して、各セッションの結果を保持します。 `Callback` というプライベート プロパティを使用して、クライアントへのコールバック チャネルにアクセスします。 次のサンプル コードに示すように、サービスはこのコールバックを使用し、コールバック インターフェイスを介してメッセージをクライアントに返信します。

[!code-csharp[c_DuplexServices#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#1)]
[!code-vb[c_DuplexServices#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#1)]

クライアントは、サービスからのメッセージを受信するために、双方向コントラクトのコールバック インターフェイスを実装するクラスを提供する必要があります。 次のサンプル コードに、`CallbackHandler` インターフェイスを実装する `ICalculatorDuplexCallback` クラスを示します。

[!code-csharp[c_DuplexServices#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#2)]
[!code-vb[c_DuplexServices#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#2)]

双方向コントラクト用に生成された WCF クライアントでは、 <xref:System.ServiceModel.InstanceContext> 構築時にクラスが提供される必要があります。 この <xref:System.ServiceModel.InstanceContext> クラスが、コールバック インターフェイスを実装するオブジェクトのサイトとして使用され、サービスから返信されるメッセージを処理します。 <xref:System.ServiceModel.InstanceContext> クラスは、`CallbackHandler` クラスのインスタンスを使用して構築されます。 このオブジェクトは、コールバック インターフェイスでサービスからクライアントに送信されるメッセージを処理します。

[!code-csharp[c_DuplexServices#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#3)]
[!code-vb[c_DuplexServices#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#3)]

サービスの構成は、セッション通信と双方向通信の両方をサポートするバインディングを提供するように設定する必要があります。 `wsDualHttpBinding` 要素はセッション通信をサポートし、どちらの方向にも HTTP 接続が 1 つ用意される双方向 HTTP 接続を提供して双方向通信を実現します。

クライアントで、サーバーがクライアントへの接続に使用するアドレスを構成する必要があります。次のサンプル構成を参照してください。

> [!NOTE]
> 非双方向クライアントがセキュリティで保護されたメッセージ交換を使用して認証に失敗した場合、通常、<xref:System.ServiceModel.Security.MessageSecurityException> がスローされます。 ただし、セキュリティで保護されたメッセージ交換を使用する双方向クライアントが認証に失敗した場合、クライアントは代わりに <xref:System.TimeoutException> を受信します。

`WSHttpBinding` 要素を使用するクライアントとサービスを作成しても、クライアントのコールバック エンドポイントが含まれていない場合は、次のエラーが発生します。

```console
HTTP could not register URL
htp://+:80/Temporary_Listen_Addresses/<guid> because TCP port 80 is being used by another application.
```

次のサンプルコードは、プログラムによってクライアントエンドポイントアドレスを指定する方法を示しています。

```csharp
WSDualHttpBinding binding = new WSDualHttpBinding();
EndpointAddress endptadr = new EndpointAddress("http://localhost:12000/DuplexTestUsingCode/Server");
binding.ClientBaseAddress = new Uri("http://localhost:8000/DuplexTestUsingCode/Client/");
```

```vb
Dim binding As New WSDualHttpBinding()
Dim endptadr As New EndpointAddress("http://localhost:12000/DuplexTestUsingCode/Server")
binding.ClientBaseAddress = New Uri("http://localhost:8000/DuplexTestUsingCode/Client/")
```

次のサンプル コードは、構成でクライアントのエンドポイント アドレスを指定する方法を示しています。

```xml
<client>
    <endpoint name ="ServerEndpoint"
          address="http://localhost:12000/DuplexTestUsingConfig/Server"
          bindingConfiguration="WSDualHttpBinding_IDuplexTest"
            binding="wsDualHttpBinding"
           contract="IDuplexTest" />
</client>
<bindings>
    <wsDualHttpBinding>
        <binding name="WSDualHttpBinding_IDuplexTest"
          clientBaseAddress="http://localhost:8000/myClient/" >
            <security mode="None"/>
         </binding>
    </wsDualHttpBinding>
</bindings>
```

> [!WARNING]
> 双方向モデルは、サービスまたはクライアントがチャネルを閉じるタイミングを自動的に検出しません。 クライアントが予期せず終了した場合、既定ではサービスに通知されません。また、サービスが予期せず終了した場合、クライアントには通知されません。 切断されているサービスを使用すると、 <xref:System.ServiceModel.CommunicationException> 例外が発生します。 クライアントとサービスは、独自のプロトコルを実装して、互いに通知するように選択できます。 エラー処理の詳細については、「 [WCF エラー処理](../wcf-error-handling.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [二重](../samples/duplex.md)
- [クライアントのランタイム動作の指定](../specifying-client-run-time-behavior.md)
- [方法: チャネル ファクトリを作成および使用して、チャネルを作成および管理する](how-to-create-a-channel-factory-and-use-it-to-create-and-manage-channels.md)
