---
title: '方法: 承認中にメタデータ要求を許可する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- allowing metadata requests while authorizing [WCF]
ms.assetid: 90cec34f-b619-452b-a056-8b1c0de49d05
ms.openlocfilehash: 6d172f9b659804179d23fb382376f83f4898edc5
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601310"
---
# <a name="how-to-allow-metadata-requests-while-authorizing"></a>方法: 承認中にメタデータ要求を許可する
カスタム承認中に、メタデータの処理要求を許可することがあります。 ここでは、このような要求を検証する手順を示します。  
  
 Windows Communication Foundation (WCF) 承認の詳細については、「[承認](authorization-in-wcf.md)」を参照してください。  
  
### <a name="to-allow-metadata-requests-during-authorization"></a>承認中にメタデータ要求を許可するには  
  
1. <xref:System.ServiceModel.ServiceAuthorizationManager> クラスの拡張を作成します。  
  
2. <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> メソッドをオーバーライドします。 このメソッドは、承認が許可されるかどうかによって、`true` または `false` を返します。 現在のプロシージャに関する情報は、メソッドへのパラメーターとして渡される <xref:System.ServiceModel.OperationContext> にあります。  
  
3. オーバーライドで、コントラクト名、名前空間、およびアクションを確認します。次の例を参照してください。 条件が有効な場合は、`true.` を返します。  
  
4. クラスを使用するための拡張ポイントを使用します。 詳細については、「[方法: サービスのカスタム承認マネージャーを作成](../extending/how-to-create-a-custom-authorization-manager-for-a-service.md)する」を参照してください。  
  
## <a name="example"></a>例  
 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> メソッドのオーバーライドを次の例に示します。  
  
 [!code-csharp[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/cs/source.cs#1)]
 [!code-vb[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/vb/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- [承認](authorization-in-wcf.md)
- [ID モデルを使用したクレームと承認の管理](managing-claims-and-authorization-with-the-identity-model.md)
