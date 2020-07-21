---
title: ClaimSet でのクレームの検索
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- claims [WCF], finding in a claimset
- claims [WCF]
ms.assetid: a76ce107-aeb3-47d0-bfa9-134c53664e20
ms.openlocfilehash: 1954da20d382630f965582fcc01bbaf72665720a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595454"
---
# <a name="finding-claims-in-a-claimset"></a>ClaimSet でのクレームの検索
クレームに基づく承認を使用する場合に、特定の種類のクレームの <xref:System.IdentityModel.Claims.ClaimSet> の内容を調べることは、一般的なタスクです。 特定のクレームが存在するかどうか、<xref:System.IdentityModel.Claims.ClaimSet> を検査するには、<xref:System.IdentityModel.Claims.ClaimSet.FindClaims%2A> メソッドを使用します。 このメソッドでは、<xref:System.IdentityModel.Claims.ClaimSet> を直接繰り返すよりも優れたパフォーマンスが得られます。 次の例は、この使用方法を示しています。 `claimType` パラメーターと `claimRight` パラメーターには `null` を指定できます。 その場合、パラメーターはすべてのクレームの種類および権限と一致します。  
  
## <a name="example"></a>例  
 [!code-csharp[c_FindClaimsPerf#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_findclaimsperf/cs/c_findclaimsperf.cs#2)]
 [!code-vb[c_FindClaimsPerf#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_findclaimsperf/vb/c_findclaimsperf.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [ID モデルを使用したクレームと承認の管理](managing-claims-and-authorization-with-the-identity-model.md)
