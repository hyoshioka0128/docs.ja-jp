---
title: '方法: WSFederationHttpBinding のセキュリティで保護されたセッションを無効にする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, federation
- federation
ms.assetid: 675fa143-6a4e-4be3-8afc-673334ab55ec
ms.openlocfilehash: df057d64feb89d1e43b938b36cb48f2f103b17d0
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595389"
---
# <a name="how-to-disable-secure-sessions-on-a-wsfederationhttpbinding"></a>方法: WSFederationHttpBinding のセキュリティで保護されたセッションを無効にする

フェデレーション資格情報を必要とするサービスの中には、セキュリティで保護されたセッションをサポートしないものがあります。 その場合は、セキュリティで保護されたセッション機能を無効にする必要があります。 <xref:System.ServiceModel.WSHttpBinding> とは異なり、<xref:System.ServiceModel.WSFederationHttpBinding> クラスでは、サービスとの通信中に、セキュリティで保護されたセッションを無効にできません。 代わりに、セキュリティで保護されたセッションの設定をブートストラップで置き換えるカスタム バインドを作成する必要があります。

ここでは、<xref:System.ServiceModel.WSFederationHttpBinding> に含まれるバインド要素を変更してカスタム バインドを作成する方法を示します。 結果は、セキュリティで保護されたセッションを使用しないことを除き、<xref:System.ServiceModel.WSFederationHttpBinding> と同じです。

## <a name="to-create-a-custom-federated-binding-without-secure-session"></a>セキュリティで保護されたセッションを使用しないカスタム フェデレーション バインディングを作成するには

1. コードで強制的に、または構成ファイルから読み込む方法によって、<xref:System.ServiceModel.WSFederationHttpBinding> クラスのインスタンスを作成します。

2. <xref:System.ServiceModel.WSFederationHttpBinding> の複製を <xref:System.ServiceModel.Channels.CustomBinding> 内に作成します。

3. <xref:System.ServiceModel.Channels.SecurityBindingElement> 内で <xref:System.ServiceModel.Channels.CustomBinding> を見つけます。

4. <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters> 内で <xref:System.ServiceModel.Channels.SecurityBindingElement> を見つけます。

5. 元の <xref:System.ServiceModel.Channels.SecurityBindingElement> を <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters> のブートストラップ セキュリティ バインド要素で置き換えます。

## <a name="example"></a>例

次の例では、セキュリティで保護されたセッションを使用しないカスタム フェデレーション バインディングを作成します。

[!code-csharp[c_CustomFederationBinding#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customfederationbinding/cs/c_customfederationbinding.cs#0)]
[!code-vb[c_CustomFederationBinding#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customfederationbinding/vb/c_customfederationbinding.vb#0)]

## <a name="compiling-the-code"></a>コードのコンパイル

- このコード例をコンパイルするには、System.ServiceModel.dll アセンブリを参照するプロジェクトを作成します。

## <a name="see-also"></a>関連項目

- [バインディングとセキュリティ](bindings-and-security.md)
