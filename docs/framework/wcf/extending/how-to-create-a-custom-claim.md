---
title: '方法: カスタム クレームを作成する'
description: WCF でカスタム要求を作成する方法について説明します。 WCF では、さまざまな組み込みの要求がサポートされており、一部のアプリケーションではカスタム要求が必要になる場合があります。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d619976b-eda3-475e-ac23-c7988a2dceb0
ms.openlocfilehash: 89f2b1359b48b71720db6ff38f27883745cfe612
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247547"
---
# <a name="how-to-create-a-custom-claim"></a>方法: カスタム クレームを作成する
Windows Communication Foundation (WCF) の Id モデルインフラストラクチャには、組み込みのクレームの種類と権限のセットが用意されて <xref:System.IdentityModel.Claims.Claim> います。これらの型と権限を使用してインスタンスを作成するためのヘルパー関数を使用します。 これらの組み込みの要求は、WCF が既定でサポートするクライアント資格情報の種類で検出された情報をモデル化するように設計されています。 多くの場合はこの組み込みクレームで十分ですが、一部のアプリケーションでカスタム クレームが必要になる場合があります。 クレームは、クレームが適用されるリソースを示すクレームの種類と、リソースにアサートされる権限で構成されます。 このトピックでは、カスタム クレームを作成する方法について説明します。  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-primitive-data-type"></a>プリミティブ データ型に基づくカスタム クレームを作成するには  
  
1. クレームの種類、リソースの値、<xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29> コンストラクターへの権限を渡すことで、カスタム クレームを作成します。  
  
    1. クレームの種類の一意の値を指定します。  
  
         クレームの種類は一意の文字列識別子です。 カスタム クレームを作成する場合、クレームの種類に使用されている文字列識別子が一意になるようにしてください。 WCF によって定義されるクレームの種類の一覧については、クラスを参照してください <xref:System.IdentityModel.Claims.ClaimTypes> 。  
  
    2. プリミティブ データ型とリソースの値を選択します。  
  
         リソースはオブジェクトです。 CLR 型のリソースにはプリミティブを指定できます。たとえば、<xref:System.String> や <xref:System.Int32>、または任意のシリアル化可能な型を指定できます。 要求は WCF によってさまざまなポイントでシリアル化されるため、リソースの CLR 型はシリアル化可能である必要があります。 プリミティブ型はシリアル化できます。  
  
    3. WCF で定義されている権限、またはカスタム権限の一意の値を選択します。  
  
         権限は一意の文字列識別子です。 WCF によって定義される権限は、クラスで定義され <xref:System.IdentityModel.Claims.Rights> ます。  
  
         カスタム クレームを作成する場合、権限に使用されている文字列識別子が一意になるようにしてください。  
  
         次のコード例では、`http://example.org/claims/simplecustomclaim` という名前のリソース用の `Driver's License` というクレームの種類と <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> 権限を持つカスタム クレームを作成します。  
  
     [!code-csharp[c_CustomClaim#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#4)]
     [!code-vb[c_CustomClaim#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#4)]  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-non-primitive-data-type"></a>プリミティブ以外のデータ型に基づくカスタム クレームを作成するには  
  
1. クレームの種類、リソースの値、<xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29> コンストラクターへの権限を渡すことで、カスタム クレームを作成します。  
  
    1. クレームの種類の一意の値を指定します。  
  
         クレームの種類は一意の文字列識別子です。 カスタム クレームを作成する場合、クレームの種類に使用されている文字列識別子が一意になるようにしてください。 WCF によって定義されるクレームの種類の一覧については、クラスを参照してください <xref:System.IdentityModel.Claims.ClaimTypes> 。  
  
    2. リソース用のシリアル化可能な、プリミティブ型以外の型を選択または定義します。  
  
         リソースはオブジェクトです。 要求は WCF によってさまざまなポイントでシリアル化されるため、リソースの CLR 型はシリアル化可能である必要があります。 プリミティブ型は既にシリアル化できます。  
  
         新しい型を作成する場合は、<xref:System.Runtime.Serialization.DataContractAttribute> をクラスに適用します。 また、クレームの一部としてシリアル化する必要のある新しい型のすべてのメンバーにも <xref:System.Runtime.Serialization.DataMemberAttribute> 属性を適用します。  
  
         `MyResourceType` というカスタム リソース型を定義するコード例を次に示します。  
  
         [!code-csharp[c_CustomClaim#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#2)]
         [!code-vb[c_CustomClaim#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#2)]
  
    3. WCF で定義されている権限、またはカスタム権限の一意の値を選択します。  
  
         権限は一意の文字列識別子です。 WCF によって定義される権限は、クラスで定義され <xref:System.IdentityModel.Claims.Rights> ます。  
  
         カスタム クレームを作成する場合、権限に使用されている文字列識別子が一意になるようにしてください。  
  
         次のコード例では、`http://example.org/claims/complexcustomclaim` というクレームの種類 (`MyResourceType` カスタム リソース型) および <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> 権限を持つカスタム クレームを作成します。  
  
         [!code-csharp[c_CustomClaim#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#5)]
         [!code-vb[c_CustomClaim#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#5)]
  
## <a name="example"></a>例  
 次のコード例で、プリミティブ リソース型を持つカスタム クレームと、プリミティブ以外のリソース型を持つカスタム クレームの作成方法を示します。  
  
 [!code-csharp[c_CustomClaim#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#0)]
 [!code-vb[c_CustomClaim#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#0)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.Rights>
- <xref:System.IdentityModel.Claims.ClaimTypes>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [ID モデルを使用したクレームと承認の管理](../feature-details/managing-claims-and-authorization-with-the-identity-model.md)
