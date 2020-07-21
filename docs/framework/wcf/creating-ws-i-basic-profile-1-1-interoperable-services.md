---
title: WS-I Basic Profile 1.1 の相互運用可能サービスの作成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- configuration [WCF], interoperable services
ms.assetid: 91b70a21-8f5c-4679-808c-2ed5fa6b2013
ms.openlocfilehash: fd7828cccb1a19a17e899525d863021d3670fbdd
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389761"
---
# <a name="creating-ws-i-basic-profile-11-interoperable-services"></a>WS-I Basic Profile 1.1 の相互運用可能サービスの作成
WCF サービス エンドポイントを構成して、Web サービス クライアントと相互運用可能ASP.NETするには、次の手順を実行します。  
  
- サービス エンドポイントのバインディングの種類として <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType> を使用する。  
  
- コールバック コントラクト機能とセッション コントラクト機能の使用、およびトランザクション動作のサービス エンドポイントでの使用をいずれも行わない。  
  
必要に応じて、HTTPS およびトランスポート レベルのクライアント認証のサポートをバインディングで有効にできます。  
  
<xref:System.ServiceModel.BasicHttpBinding> クラスの次の機能を使用する場合、WS-I Basic Profile 1.1 の機能では十分ではありません。  
  
- <xref:System.ServiceModel.BasicHttpBinding.MessageEncoding%2A?displayProperty=nameWithType> プロパティで制御される MTOM (Message Transmission Optimization Mechanism) メッセージ エンコーディング。 MTOM を使用しない場合は、このプロパティを既定値 (<xref:System.ServiceModel.WSMessageEncoding.Text?displayProperty=nameWithType>) のままにしておきます。  
  
- <xref:System.ServiceModel.BasicHttpBinding.Security%2A?displayProperty=nameWithType> 値によって制御されるメッセージ セキュリティでは、WS-I Basic Security Profile 1.0 に準拠した WS-Security がサポートされます。 WS-Security を使用しない場合は、このプロパティを既定値 (<xref:System.ServiceModel.SecurityMode.Transport?displayProperty=nameWithType>) のままにしておきます。  
  
WCF サービスのメタデータをASP.NETで使用できるようにするには、Web サービスのクライアント生成ツールである[Web サービス記述言語ツール (Wsdl.exe)、Web](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7h3ystb6%28v=vs.100%29)[サービス探索ツール (Disco.exe)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cy2a3ybs%28v=vs.100%29)、および Visual Studio の**Web 参照の追加**機能を使用します。 メタデータの公開を有効にします。 詳細については、「メタデータ[エンドポイントの公開](publishing-metadata-endpoints.md)」を参照してください。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、ASP.NET Web サービス クライアントと互換性のある WCF エンドポイントをコード内および構成ファイルに追加する方法を示します。  
  
### <a name="code"></a>コード  
 [!code-csharp[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/cs/program.cs#0)]
 [!code-vb[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/vb/program.vb#0)]  
 [!code-xml[C_HowTo-WCFServiceAndASMXClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/common/app.config#1)]  
  
## <a name="see-also"></a>関連項目

- [ASP.NET Web サービスとの相互運用](./feature-details/interop-with-aspnet-web-services.md)
