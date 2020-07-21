---
title: クレームの作成とリソース値
ms.date: 03/30/2017
helpviewer_keywords:
- claims [WCF], creation and resource values
ms.assetid: 30431f76-cbe7-4bad-bad7-8e43e23a82d4
ms.openlocfilehash: fabd0a2606560d99174e5ad28940c3b59ee689d9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587054"
---
# <a name="claim-creation-and-resource-values"></a>クレームの作成とリソース値
<xref:System.IdentityModel.Claims.Claim> クラスには、組み込みのクレームの種類のインスタンスを作成するためのメソッドが複数用意されています。 これらのメソッドの中でも、次のものは指定されたリソースに対してセマンティックまたは形式のチェックを行いません。  
  
- <xref:System.IdentityModel.Claims.Claim.CreateDnsClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateHashClaim%2A> (長さまたはバイト配列のコンテンツは検査されません)  
  
- <xref:System.IdentityModel.Claims.Claim.CreateNameClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateSpnClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateThumbprintClaim%2A> (長さまたはバイト配列のコンテンツは検査されません)  
  
- <xref:System.IdentityModel.Claims.Claim.CreateUpnClaim%2A>  
  
 上記のメソッドを使用する場合は、渡されるリソース値が正しい形式である、または正しい情報を含んでいること (あるいは両方) を確認するように注意してください。  
  
 次のメソッドは、特定の型を受け取ります。  
  
- <xref:System.IdentityModel.Claims.Claim.CreateDenyOnlyWindowsSidClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateMailAddressClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateRsaClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateUriClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateWindowsSidClaim%2A>  
  
- <xref:System.IdentityModel.Claims.Claim.CreateX500DistinguishedNameClaim%2A>  
  
## <a name="see-also"></a>関連項目

- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.ClaimSet>
- [ID モデルを使用したクレームと承認の管理](managing-claims-and-authorization-with-the-identity-model.md)
