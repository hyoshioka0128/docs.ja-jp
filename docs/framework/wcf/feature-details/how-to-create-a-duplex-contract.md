---
title: '方法: 双方向コントラクトを作成する'
description: WCF クライアントとサーバーが互いに独立して通信できるようにする、双方向コントラクトを作成する方法について説明します。 どちらも、もう一方の呼び出しを開始できます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- duplex contracts [WCF]
ms.assetid: 500a75b6-998a-47d5-8e3b-24e3aba2a434
ms.openlocfilehash: 9320e5b36b8faba3602fbe1df1b95c05dcc7fa7e
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247092"
---
# <a name="how-to-create-a-duplex-contract"></a>方法: 双方向コントラクトを作成する
ここでは、双方向コントラクトを使用するメソッドを作成するための基本手順を示します。 双方向コントラクトでは、クライアントとサーバーが互いに独立して通信できるため、どちらからでも相手の呼び出しを開始できます。 双方向コントラクトは、Windows Communication Foundation (WCF) サービスで使用可能な3つのメッセージパターンのうちの1つです。 他の 2 つのメッセージ パターンは、一方向および要求/応答です。 双方向コントラクトは、クライアントとサーバー間の 2 つの一方向コントラクトで構成され、メソッドの呼び出しが相互に関連付けられている必要はありません。 サービスでクライアントに詳細を照会したり、クライアントで明示的にイベントを発生させたりする必要がある場合は、この種のコントラクトを使用します。 双方向コントラクト用のクライアントアプリケーションを作成する方法の詳細については、「[方法: 双方向コントラクトを使用してサービスにアクセスする](how-to-access-services-with-a-duplex-contract.md)」を参照してください。 実際のサンプルについては、[二重](../samples/duplex.md)サンプルを参照してください。  
  
### <a name="to-create-a-duplex-contract"></a>双方向コントラクトを作成するには  
  
1. 双方向コントラクトのサーバー側を構成するインターフェイスを作成します。  
  
2. インターフェイスに <xref:System.ServiceModel.ServiceContractAttribute> クラスを適用します。  
  
     [!code-csharp[S_WS_DualHttp#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#3)]
     [!code-vb[S_WS_DualHttp#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#3)]  
  
3. インターフェイスでメソッド署名を宣言します。  
  
4. パブリック コントラクトの一部であることが必要な各メソッド シグネチャに、<xref:System.ServiceModel.OperationContractAttribute> クラスを適用します。  
  
5. クライアントでサービスが呼び出すことができる一連の操作を定義するコールバック インターフェイスを作成します。  
  
     [!code-csharp[S_WS_DualHttp#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#4)]
     [!code-vb[S_WS_DualHttp#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#4)]  
  
6. コールバック インターフェイスでメソッド署名を宣言します。  
  
7. パブリック コントラクトの一部であることが必要な各メソッド シグネチャに、<xref:System.ServiceModel.OperationContractAttribute> クラスを適用します。  
  
8. プライマリ インターフェイスの <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A> プロパティをコールバック インターフェイスの型に設定することにより、2 つのインターフェイスを双方向コントラクトにリンクします。  
  
### <a name="to-call-methods-on-the-client"></a>クライアントでメソッドを呼び出すには  
  
1. サービスのプライマリ コントラクトの実装で、コールバック インターフェイスの変数を宣言します。  
  
2. <xref:System.ServiceModel.OperationContext.GetCallbackChannel%2A> クラスの <xref:System.ServiceModel.OperationContext> メソッドから返されるオブジェクト参照に変数を設定します。  
  
     [!code-csharp[S_WS_DualHttp#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#1)]
     [!code-vb[S_WS_DualHttp#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#1)]  
  
     [!code-csharp[S_WS_DualHttp#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#2)]
     [!code-vb[S_WS_DualHttp#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#2)]  
  
3. コールバック インターフェイスで定義されたメソッドを呼び出します。  
  
## <a name="example"></a>例  
 次のコード例は、双方向通信を示しています。 サービスのコントラクトには、順方向および逆方向に移動するためのサービス操作が含まれます。 クライアントのコントラクトには、位置を報告するためのサービス操作が含まれます。  
  
 [!code-csharp[S_WS_DualHttp#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#5)]
 [!code-vb[S_WS_DualHttp#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#5)]  
  
- <xref:System.ServiceModel.ServiceContractAttribute> 属性と <xref:System.ServiceModel.OperationContractAttribute> 属性を適用すると、サービス コントラクトの定義を Web サービス記述言語 (WSDL) で自動的に生成できます。  
  
- [ServiceModel メタデータユーティリティツール (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用して、クライアントの WSDL ドキュメントおよび (省略可能な) コードと構成を取得します。  
  
- 双方向サービスを公開しているエンドポイントは、セキュリティで保護されている必要があります。 サービスが双方向メッセージを受信すると、その受信メッセージの ReplyTo を参照して応答の送信先を決定します。 チャネルがセキュリティで保護されていない場合、信頼関係のないクライアントが対象コンピューターの ReplyTo を使用して悪意のあるメッセージを送信し、その対象コンピューターのサービス拒否 (DOS: Denial Of Service) を引き起こす可能性があります。 通常の要求/応答メッセージでは、ReplyTo は無視され、元のメッセージを受信したチャネルで応答が送信されます。したがって、この問題は発生しません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [方法: 双方向コントラクトを使用してサービスにアクセスする](how-to-access-services-with-a-duplex-contract.md)
- [二重](../samples/duplex.md)
- [サービスの設計と実装](../designing-and-implementing-services.md)
- [方法: サービス コントラクトを定義する](../how-to-define-a-wcf-service-contract.md)
- [セッション](../samples/session.md)
