---
title: コンテキスト交換プロトコル
ms.date: 03/30/2017
ms.assetid: 3dfd38e0-ae52-491c-94f4-7a862b9843d4
ms.openlocfilehash: 86d2a19b086fbd5d6be6f1a084bfd7aaace0e250
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597437"
---
# <a name="context-exchange-protocol"></a>コンテキスト交換プロトコル
このセクションでは、Windows Communication Foundation (WCF) リリース .NET Framework バージョン3.5 で導入されたコンテキスト交換プロトコルについて説明します。 このプロトコルを使用すると、クライアント チャネルはサービスから送られたコンテキストを受け入れ、以降はそのコンテキストを、同じクライアント チャネル インスタンス経由でそのサービスに送信されるすべての要求に適用できます。 コンテキスト交換プロトコルを実装されると、2 つの機構 (HTTP クッキーまたは SOAP ヘッダー) のいずれか 1 つを使用し、サーバーとクライアント間でコンテキストを伝達できます。  
  
 コンテキスト交換プロトコルは、カスタム チャネル層に実装されます。 チャネルでは <xref:System.ServiceModel.Channels.ContextMessageProperty> プロパティを使用して、アプリケーション層とコンテキストを送受信します。 エンドポイント間の転送については、コンテキストの値は、チャネル層で SOAP ヘッダーとしてシリアル化されるか、HTTP 要求および応答を表すメッセージ プロパティとの間で双方向に変換されます。 後者の場合、下位のチャネル層のいずれか 1 つで、HTTP 要求および応答のメッセージ プロパティをそれぞれ HTTP クッキーとの間で双方向に変換する必要があります。 コンテキスト交換に使用する機構の選択は、<xref:System.ServiceModel.Channels.ContextExchangeMechanism> の <xref:System.ServiceModel.Channels.ContextBindingElement> プロパティを使用します。 有効な値は `HttpCookie` または `SoapHeader`です。  
  
 クライアントでは、チャネルのインスタンスは <xref:System.ServiceModel.Channels.IContextManager.Enabled%2A> チャネル プロパティの設定値に基づいて 2 つのモードで動作します。  
  
## <a name="mode-1-channel-context-management"></a>モード 1: チャネル コンテキスト管理  
 これは、<xref:System.ServiceModel.Channels.IContextManager.Enabled%2A> を `true` に設定した場合の既定のモードです。 このモードでは、コンテキスト チャネルはコンテキストを管理し、その有効期間中、コンテキストをキャッシュします。 コンテキストは、`IContextManager` メソッドを呼び出して、`GetContext` チャネル プロパティ経由でチャネルから取得できます。 チャネルを開く前に、チャネル プロパティで `SetContext` メソッドを呼び出して、事前に特定のコンテキストで初期化できます。 チャネルは一度コンテキストで初期化すると、リセットできません。  
  
 このモードのインバリアントの一覧を次に示します。  
  
- チャネルを開いた後に `SetContext` を使用してコンテキストをリセットしようとすると、<xref:System.InvalidOperationException> がスローされます。  
  
- 送信メッセージで <xref:System.ServiceModel.Channels.ContextMessageProperty> を使用してコンテキストを送信しようとすると、<xref:System.InvalidOperationException> がスローされます。  
  
- 特定のコンテキストを持つサーバーからメッセージを受信する場合に、チャネルが既に特定のコンテキストで初期化されていると、<xref:System.ServiceModel.ProtocolException> が発生します。  
  
    > [!NOTE]
    > 明示的にコンテキストが設定されていないチャネルを開いている場合に限り、サーバーから初期コンテキストを受信するのが適切です。  
  
- 受信メッセージの <xref:System.ServiceModel.Channels.ContextMessageProperty> は常に null です。  
  
## <a name="mode-2-application-context-management"></a>モード 2: アプリケーション コンテキスト管理  
 これは、<xref:System.ServiceModel.Channels.IContextManager.Enabled%2A> を `false` に設定した場合のモードです。 このモードでは、コンテキスト チャネルでコンテキストを管理しません。 コンテキストの取得、管理、および適用は、<xref:System.ServiceModel.Channels.ContextMessageProperty> を使用してアプリケーションで行う必要があります。 `GetContext` または `SetContext` を呼び出そうとすると、<xref:System.InvalidOperationException> が発生します。  
  
 どちらのモードを選択しても、クライアント チャネル ファクトリは、<xref:System.ServiceModel.Channels.IRequestChannel>、<xref:System.ServiceModel.Channels.IRequestSessionChannel>、および <xref:System.ServiceModel.Channels.IDuplexSessionChannel> の各メッセージ交換パターンをサポートします。  
  
 サービスでは、チャネルのインスタンスが、受信メッセージでクライアントから送られたコンテキストを <xref:System.ServiceModel.Channels.ContextMessageProperty> に変換します。 これで、アプリケーション層、または呼び出しスタックの上位に位置する他のチャネルから、メッセージ プロパティにアクセスできるようになります。 サービス チャネルを使用し、応答メッセージに <xref:System.ServiceModel.Channels.ContextMessageProperty> をアタッチすることによって、クライアントに返される新しいコンテキスト値をアプリケーション層で指定することもできます。 このプロパティは、コンテキストを含む SOAP ヘッダーまたは HTTP クッキーに変換されます。どちらに変換されるかは、バイディングの構成によって決まります。 サービス チャネル リスナーは、<xref:System.ServiceModel.Channels.IReplyChannel>、<xref:System.ServiceModel.Channels.IReplySessionChannel>、および <xref:System.ServiceModel.Channels.IReplySessionChannel> の各メッセージ交換パターンをサポートします。  
  
 コンテキスト交換プロトコルは、コンテキストの伝達に HTTP クッキーを使用しない場合にコンテキスト情報を表す新しい `wsc:Context` SOAP ヘッダーを使用します。 コンテキスト ヘッダー スキーマでは、文字列キーと文字列コンテンツを持つ任意の数の子要素を使用できます。 コンテキスト ヘッダーの例を次に示します。  
  
 `<Context xmlns="http://schemas.microsoft.com/ws/2006/05/context">`  
  
 `<property name="myContext">context-2</property>`  
  
 `</Context>`  
  
 `HttpCookie` モードの場合、`SetCookie` ヘッダーを使用してクッキーが設定されます。 クッキーの名前は `WscContext` です。 クッキーの値は、`wsc:Context` ヘッダーの Base64 エンコーディングです。 この値は引用符で囲まれます。  
  
 WS-Addressing ヘッダーを保護するのと同じ理由により、コンテキスト値は、転送中に変更されないように保護する必要があります。WS-Addressing ヘッダーは、サービスで要求のディスパッチ先を確認するのに使用されます。 したがって、バインディングにメッセージ保護機能がある場合、SOAP レベルかトランスポート レベルのいずれかで `wsc:Context` ヘッダーにデジタル署名するか、署名と暗号化を行う必要があります。 HTTP クッキーを使用してコンテキストを伝達する場合は、トランスポート セキュリティを使用して保護する必要があります。  
  
 サービス エンドポイントでコンテキスト交換プロトコルのサポートを必要とする場合は、公開するポリシーにそのことを明示できます。 新たに 2 つのポリシー アサーションが導入され、SOAP レベルでコンテキスト交換プロトコルをサポートしたり、HTTP クッキーのサポートを有効化したりするクライアント要件を示すことができます。 このアサーションはサービスのポリシー内に生成されます。生成は次のように、<xref:System.ServiceModel.Channels.ContextBindingElement.ContextExchangeMechanism%2A> プロパティの値によって制御します。  
  
- <xref:System.ServiceModel.Channels.ContextExchangeMechanism.ContextSoapHeader> の場合は、次のアサーションが生成されます。  
  
    ```xml  
    <IncludeContext
    xmlns="http://schemas.microsoft.com/ws/2006/05/context"  
    protectionLevel="Sign" />  
    ```  
  
- <xref:System.ServiceModel.Channels.ContextExchangeMechanism.HttpCookie> の場合は、次のアサーションが生成されます。  
  
    ```xml  
    <HttpUseCookie xmlns="http://schemas.xmlsoap.org/soap/http"/>  
    ```  
  
## <a name="see-also"></a>関連項目

- [Web サービス プロトコルの相互運用性ガイド](web-services-protocols-interoperability-guide.md)
