---
title: '方法: 一方向コントラクトを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 85084cd9-31cc-4e95-b667-42ef01336622
ms.openlocfilehash: 42c056c9b56ed1245290cd66833cc6565f517b66
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593452"
---
# <a name="how-to-create-a-one-way-contract"></a>方法: 一方向コントラクトを作成する
ここでは、一方向コントラクトを使用するメソッドを作成するための基本手順を示します。 このようなメソッドは、クライアントから Windows Communication Foundation (WCF) サービスに対して操作を呼び出しますが、応答を想定していません。 この種のコントラクトは、たとえば、多数のサブスクライバーに対して通知を発行するために使用できます。 一方向コントラクトは、二重のコントラクトを作成する場合にも使用できます。その場合は、クライアントとサーバーが互いに独立して通信できるため、どちらからでも相手の呼び出しを開始できます。 これにより、特にサーバーは、クライアントがイベントとして処理できる一方向の呼び出しをクライアントに対して実行できます。 一方向メソッドの指定の詳細については、<xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> プロパティおよび <xref:System.ServiceModel.OperationContractAttribute> クラスのトピックを参照してください。  
  
 双方向コントラクト用のクライアントアプリケーションを作成する方法の詳細については、「[方法: 一方向コントラクトと要求/応答コントラクトを使用してサービスにアクセスする](how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)」を参照してください。 実際のサンプルについては、[一方向](../samples/one-way.md)のサンプルを参照してください。  
  
### <a name="to-create-a-one-way-contract"></a>一方向コントラクトを作成するには  
  
1. サービスにより実装されるメソッドを定義するインターフェイスに <xref:System.ServiceModel.ServiceContractAttribute> クラスを適用することにより、サービス コントラクトを作成します。  
  
2. <xref:System.ServiceModel.OperationContractAttribute> クラスをメソッドに適用する際に、クライアントが呼び出すことのできるインターフェイスのメソッドを指定します。  
  
3. <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> プロパティを `true` に設定することにより、出力を行わない (戻り値および出力または参照パラメーターを持たない) 一方向の操作を指定します。 <xref:System.ServiceModel.OperationContractAttribute> プロパティの既定値は <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> であるため、`false` クラスを持つ操作では、既定で要求/応答コントラクトが満たされることに注意してください。 したがって、このメソッドに一方向コントラクトが必要な場合は、この属性プロパティの値を明示的に `true` に指定する必要があります。  
  
## <a name="example"></a>例  
 複数の一方向メソッドを含むサービスのコントラクトを定義する方法を次のコード例に示します。 `Equals` (既定で応答/要求コントラクトに設定され、結果を返します) を除き、すべてのメソッドは一方向コントラクトを持ちます。  
  
 [!code-csharp[S_Service_Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [サービスの設計と実装](../designing-and-implementing-services.md)
- [方法: サービス コントラクトを定義する](../how-to-define-a-wcf-service-contract.md)
- [セッション](../samples/session.md)
- [方法: 双方向コントラクトを作成する](how-to-create-a-duplex-contract.md)
