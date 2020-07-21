---
title: リソースへのアクセスのクレームと拒否
ms.date: 03/30/2017
helpviewer_keywords:
- claims [WCF], denying access to resources
ms.assetid: 145ebb41-680e-4256-b14c-1efb4af1e982
ms.openlocfilehash: e5ecb71b7e0596b1732207b50e1b6087528bba3f
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587041"
---
# <a name="claims-and-denying-access-to-resources"></a>リソースへのアクセスのクレームと拒否
Windows Communication Foundation (WCF) は、クレームベースの承認メカニズムをサポートしています。 クレームの有無に応じてリソースへのアクセスが許可されるばかりでなく、クレームの有無に応じてリソースへのアクセスがシステムによって拒否される場合もよくあります。 このようなシステムでは、アクセスが許可された要求を探す前に、アクセスが拒否されたクレームの <xref:System.IdentityModel.Policy.AuthorizationContext> を調べる必要があります。  
  
 たとえば、`Age` 型、<xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> 権限、`Under 21` リソース値というクレームを持つ任意のユーザーに対してリソースへのアクセスを拒否し、ID が `Name` 型、<xref:System.IdentityModel.Claims.Rights.Identity%2A> 権限、`Mallory` リソース値というクレームを持っている場合にのみ、リソースへのアクセスを許可するとします。 言い換えると、年齢が 21 歳以下の任意のユーザーはシステムによってアクセスが拒否され、名前が Mallory である任意のユーザーにはアクセスが許可されるようにします。 この意味を正しく実装するには、`Age` クレームを最初に探して、ユーザーが 21 歳以下であるかどうかを判断することが重要です。 そうしないと、Mallory が 21 歳以下である場合、このリソースには、`Name` クレームのみに基づいてアクセスが許可されてしまいます。  
  
## <a name="see-also"></a>関連項目

- [ID モデルを使用したクレームと承認の管理](managing-claims-and-authorization-with-the-identity-model.md)
- [クレームとトークン](claims-and-tokens.md)
