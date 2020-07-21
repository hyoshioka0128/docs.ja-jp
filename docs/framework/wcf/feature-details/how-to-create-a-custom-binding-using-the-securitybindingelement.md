---
title: '方法: SecurityBindingElement を使用してカスタム バインドを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], creating custom bindings
ms.assetid: 203a9f9e-3a73-427c-87aa-721c56265b29
ms.openlocfilehash: 15fdd50b05bd2217cb9819373cd1c015da52b15b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599010"
---
# <a name="how-to-create-a-custom-binding-using-the-securitybindingelement"></a>方法: SecurityBindingElement を使用してカスタム バインドを作成する
Windows Communication Foundation (WCF) には、構成できるシステム指定のバインディングがいくつか用意されていますが、WCF がサポートするすべてのセキュリティオプションを構成するときに完全な柔軟性は提供されません。 ここでは、個別のバインド要素からカスタム バインディングを直接作成する方法を説明し、このようなバインディングを作成する場合に指定できるセキュリティ設定のいくつかに焦点を当てます。 カスタムバインディングの作成の詳細については、「[バインディングの拡張](../extending/extending-bindings.md)」を参照してください。  
  
> [!WARNING]
> <xref:System.ServiceModel.Channels.SecurityBindingElement> では、<xref:System.ServiceModel.Channels.IDuplexSessionChannel> が <xref:System.ServiceModel.TransferMode> に設定されている場合に TCP トランスポートによって使用される既定のチャネル形状である <xref:System.ServiceModel.TransferMode.Buffered> チャネル形状をサポートしていません。 このシナリオで <xref:System.ServiceModel.TransferMode> を使用するには、<xref:System.ServiceModel.TransferMode.Streamed> を <xref:System.ServiceModel.Channels.SecurityBindingElement> に設定する必要があります。  
  
## <a name="creating-a-custom-binding"></a>カスタム バインドの作成  
 WCF では、すべてのバインドは*バインド要素*で構成されます。 各バインド要素は <xref:System.ServiceModel.Channels.BindingElement> クラスから派生します。 標準のシステム指定のバインディングの場合、バインド要素は自動的に作成および構成されます。ただし、プロパティ設定の一部はカスタマイズが可能です。  
  
 これに対し、カスタム バインドを作成する場合は、バインド要素が作成および構成され、そのバインド要素から <xref:System.ServiceModel.Channels.CustomBinding> が作成されます。  
  
 これを行うには、<xref:System.ServiceModel.Channels.BindingElementCollection> クラスのインスタンスによって表されるコレクションに個別のバインド要素を追加し、`Elements` の `CustomBinding` プロパティをそのオブジェクトと同じにします。 バインド要素は、トランザクション フロー、信頼できるセッション、セキュリティ、複合二重、一方向、ストリーム セキュリティ、メッセージ エンコーディング、トランスポートの順に追加する必要があります。 どのバインディングでも、これらすべてのバインド要素が必要になるとは限りません。  
  
## <a name="securitybindingelement"></a>SecurityBindingElement  
 3 つのバインド要素がメッセージ レベルのセキュリティに関連しており、これらはすべて <xref:System.ServiceModel.Channels.SecurityBindingElement> クラスから派生します。 この 3 つのバインディングとは、<xref:System.ServiceModel.Channels.TransportSecurityBindingElement>、<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>、および <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> です。 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement> は混合モード セキュリティを提供するために使用されます。 他の 2 つの要素は、メッセージ層でセキュリティを提供する場合に使用します。  
  
 トランスポート レベルのセキュリティが提供される場合は、次の追加のクラスが使用されます。  
  
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
- <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
- <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
## <a name="required-binding-elements"></a>必要なバインド要素  
 1 つのバインディングに結合できる可能性のあるバインド要素は多数存在します。 これらの組み合わせすべてが有効なわけではありません。 ここでは、セキュリティ バインディングに存在する必要のある要素について説明します。  
  
 有効なセキュリティ バインディングは、次のような多くの要因に依存します。  
  
- セキュリティ モード  
  
- トランスポート プロトコル  
  
- コントラクトに指定されているメッセージ交換パターン (MEP)  
  
 前述の要因の各組み合わせに有効なバインド要素のスタックの構成を次の表に示します。 これらは最小限の要件であることに注意してください。 メッセージ エンコーディング バインド要素、トランザクション バインド要素などの追加のバインド要素をバインディングに追加することもできます。  
  
|セキュリティ モード|トランスポート|コントラクトのメッセージ交換パターン|コントラクトのメッセージ交換パターン|コントラクトのメッセージ交換パターン|  
|-------------------|---------------|---------------------------------------|---------------------------------------|---------------------------------------|  
|||`Datagram`|`Request Reply`|`Duplex`|  
|トランスポート|Https||||  
|||OneWayBindingElement|||  
|||HttpsTransportBindingElement|HttpsTransportBindingElement||  
||TCP||||  
|||OneWayBindingElement|||  
|||SSL または Windows StreamSecurityBindingElement|SSL または Windows StreamSecurityBindingElement|SSL または Windows StreamSecurityBindingElement|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
|Message|Http|SymmetricSecurityBindingElement|SymmetricSecurityBindingElement|SymmetricSecurityBindingElement (認証モード = SecureConversation)|  
|||||CompositeDuplexBindingElement|  
|||OneWayBindingElement||OneWayBindingElement|  
|||HttpTransportBindingElement|HttpTransportBindingElement|HttpTransportBindingElement|  
||Tcp|SecurityBindingElement|SecurityBindingElement|SymmetricSecurityBindingElement (認証モード = SecureConversation)|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
|混合 (メッセージ資格情報付きトランスポート)|Https|TransportSecurityBindingElement|TransportSecurityBindingElement||  
|||OneWayBindingElement|||  
|||HttpsTransportBindingElement|HttpsTransportBindingElement||  
||TCP|TransportSecurityBindingElement|SymmetricSecurityBindingElement (認証モード = SecureConversation)|SymmetricSecurityBindingElement (認証モード = SecureConversation)|  
|||OneWayBindingElement|||  
|||SSL または Windows StreamSecurityBindingElement|SSL または Windows StreamSecurityBindingElement|SSL または Windows StreamSecurityBindingElement|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
  
 SecurityBindingElements には構成可能な設定が多数あることに注意してください。 詳細については、「[認証モード](securitybindingelement-authentication-modes.md)の使用」を参照してください。  
  
 詳細については、「[セキュリティで保護された通信とセッション](secure-conversations-and-secure-sessions.md)」を参照してください。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-create-a-custom-binding-that-uses-a-symmetricsecuritybindingelement"></a>SymmetricSecurityBindingElement を使用するカスタム バインディングを作成するには  
  
1. <xref:System.ServiceModel.Channels.BindingElementCollection> クラスのインスタンスを `outputBec` という名前で作成します。  
  
2. 静的メソッド `M:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationBindingElement(true)` を呼び出します。このメソッドは、<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> クラスのインスタンスを返します。  
  
3. <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> クラスの `outputBec` の `Add` メソッドを呼び出して、<xref:System.Collections.ObjectModel.Collection%601> をコレクション (<xref:System.ServiceModel.Channels.BindingElement>) に追加します。  
  
4. <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> クラスのインスタンスを作成し、これをコレクション (`outputBec`) に追加します。 これにより、バインディングによって使用されるエンコーディングが指定されます。  
  
5. <xref:System.ServiceModel.Channels.HttpTransportBindingElement> を作成し、これをコレクション (`outputBec`) に追加します。 これにより、バインディングが HTTP トランスポートを使用することが指定されます。  
  
6. <xref:System.ServiceModel.Channels.CustomBinding> クラスのインスタンスを作成し、コレクション `outputBec` をコンストラクターに渡して、新規のカスタム バインドを作成します。  
  
7. 作成されたカスタム バインドは、標準の <xref:System.ServiceModel.WSHttpBinding> と同じ特性を数多く共有しています。 カスタム バインディングではメッセージ レベルのセキュリティと Windows 資格情報が指定されていますが、セキュリティで保護されたセッションは無効になっているため、サービス資格情報が帯域外で指定される必要があり、また署名も暗号化されません。 署名の暗号化は、<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A> プロパティを手順 4. で示したように設定することでのみ制御できます。 他の 2 つについては、標準バインディングの設定を使用することで制御できます。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例では、<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> を使用するカスタム バインドを作成する関数全体を示します。  
  
### <a name="code"></a>コード  
 [!code-csharp[c_CustomBinding#20](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#20)]
 [!code-vb[c_CustomBinding#20](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_custombinding/vb/source.vb#20)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Channels.SecurityBindingElement>
- <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>
- <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [バインディングの拡張](../extending/extending-bindings.md)
- [システム標準のバインディング](../system-provided-bindings.md)
