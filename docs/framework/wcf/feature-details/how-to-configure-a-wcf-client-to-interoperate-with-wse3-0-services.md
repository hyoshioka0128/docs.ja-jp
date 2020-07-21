---
title: '方法: WCF クライアントと WSE3.0 サービスを相互運用するために構成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3dadd7f1-d207-4ea5-a73b-3e8aa44407f8
ms.openlocfilehash: 7dd50fcc07c6c090042cf87acb4aa5d2b5321a68
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84579580"
---
# <a name="how-to-configure-a-wcf-client-to-interoperate-with-wse30-services"></a>方法: WCF クライアントと WSE3.0 サービスを相互運用するために構成する
Windows Communication Foundation (WCF) クライアントは、WS-ADDRESSING 仕様の8月2004バージョンを使用するように WCF クライアントが構成されている場合に、Web サービス拡張 Microsoft .NET 3.0 (WSE) サービスとのワイヤレベルの互換性があります。  
  
### <a name="to-configure-a-wcf-client-to-interoperate-with-a-wse-30-web-service"></a>WSE 3.0 Web サービスと相互運用するように WCF クライアントを構成するには  
  
1. [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を実行して、WSE 3.0 Web サービス用の WCF クライアントを作成します。  
  
     WSE Web サービスの場合は、WCF クライアントクラスが作成されます。  
  
     WCF クライアントの作成の詳細については、「[方法: クライアントを作成](../how-to-create-a-wcf-client.md)する」を参照してください。  
  
2. WSE 3.0 Web サービスと通信できるバインディングを表すクラスを作成します。  
  
     次のクラスは、 [WSE との相互運用](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29)のサンプルに含まれています。  
  
    1. <xref:System.ServiceModel.Channels.Binding> クラスから派生するクラスを作成します。  
  
         `WseHttpBinding` クラスから派生する、<xref:System.ServiceModel.Channels.Binding> という名前のクラスを作成する方法を次のコード例に示します。  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2. WSE の設定不要アサーションを指定するクラスに、派生キーが必要か、セキュリティで保護されたセッションが使用されるか、署名の確認が必要かどうかの指定、およびメッセージ保護設定などのプロパティを追加します。  
  
         次のコード例では `SecurityAssertion` 、、、、およびの各プロパティを定義し `RequireDerivedKeys` `EstablishSecurityContext` `MessageProtectionOrder` ます。 WSE のターンキーアサーション、派生キーが必要かどうか、セキュリティで保護されたセッションを使用するかどうか、署名の確認が必要かどうか、およびメッセージ保護設定を指定します。  
  
         [!code-csharp[c_WCFClientToWSEService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#3)]
         [!code-vb[c_WCFClientToWSEService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#3)]  
  
    3. <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> メソッドをオーバーライドして、バインディング プロパティを設定します。  
  
         `SecurityAssertion` プロパティと `MessageProtectionOrder` プロパティの値を取得することで、トランスポート、メッセージ エンコーディング、メッセージ保護設定を指定するコード例を次に示します。  
  
         [!code-csharp[c_WCFClientToWSEService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#2)]
         [!code-vb[c_WCFClientToWSEService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#2)]  
  
3. クライアントのアプリケーション コードでは、コードを追加してバインディングのプロパティを設定します。  
  
     次のコード例では、WCF クライアントで、WSE 3.0 のターンキーセキュリティアサーションによる定義に従ってメッセージの保護と認証を使用する必要があることを指定し `AnonymousForCertificate` ます。 また、セキュリティで保護されたセッションと派生キーが必要です。  
  
     [!code-csharp[c_WCFClientToWSEService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#4)]
     [!code-vb[c_WCFClientToWSEService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#4)]  
  
## <a name="example"></a>例  
 WSE 3.0 の設定不要のセキュリティ アサーションのプロパティに対応するプロパティを公開するカスタムのバインディングを定義するコード例を次に示します。 次に、という名前のカスタムバインディングを使用して、 `WseHttpBinding` WCF クライアントのバインディングプロパティを指定します。  

[!code-csharp[c_WCFClientToWSEService#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#0)]
[!code-vb[c_WCFClientToWSEService#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#0)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Channels.Binding>
- [WSE との相互運用](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29)
