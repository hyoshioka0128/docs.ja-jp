---
title: 電子署名の暗号化
ms.date: 03/30/2017
helpviewer_keywords:
- encryption of digital signatures [WCF]
- digital signatures [WCF], encryption
- digital signatures [WCF]
ms.assetid: 0868866d-40b4-4341-8e42-eee3b7f15b69
ms.openlocfilehash: 41094b2eee50e97cf60887cfa29f8110f2895bfa
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597398"
---
# <a name="encryption-of-digital-signatures"></a>電子署名の暗号化
既定では、メッセージは署名および暗号化され、署名はデジタル暗号化されます。 これは、<xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> または <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> のインスタンスを使用してカスタム バインドを作成し、いずれかのクラスの `MessageProtectionOrder` プロパティを <xref:System.ServiceModel.Security.MessageProtectionOrder> 列挙値に設定することによって制御できます。 既定値は、<xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncryptAndEncryptSignature> です。 このプロセスは、単に署名して暗号化する場合よりも時間が 10 ～ 40 % 長くかかります。 ただし、署名の暗号化を無効にすると、攻撃者がメッセージの内容を予想できるようになる恐れがあります。 その理由は、メッセージ内のすべての署名部分のプレーン テキストのハッシュ コードが署名要素に含まれるからです。 たとえば、メッセージ本体は既定で暗号化されますが、暗号化されていない署名には、メッセージ本体のハッシュ コードが含まれます。 メッセージが短い場合は、攻撃者に内容を推測されてしまうおそれがあります。 署名を暗号化すると、このような危険性が低減または解消されます。  
  
 そのため、署名の暗号化を無効にするのは、セキュリティに影響しない大型のバイナリ ファイルを送信する場合などの、内容の重要性が低く、パフォーマンスの向上が重要な場合に限定してください。  
  
### <a name="to-disable-digital-signing"></a>デジタル署名を無効にするには  
  
1. <xref:System.ServiceModel.Channels.CustomBinding> を作成します。 詳細については、「[方法: カスタムバインディングを使用してカスタムバインディングを作成](how-to-create-a-custom-binding-using-the-securitybindingelement.md)する」を参照してください。  
  
2. <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> または <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> をバインディング コレクションに追加します。  
  
3. <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=nameWithType> プロパティを <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt> に設定するか、または <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A?displayProperty=nameWithType> プロパティを <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt> に設定します。  
  
 カスタムバインディングの作成の詳細については、「[ユーザー定義バインディングの作成](../extending/creating-user-defined-bindings.md)」を参照してください。 特定の認証モード用のカスタムバインディングを作成する方法の詳細については、「[方法: 指定した認証モードのための](how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)内容を作成する」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Security.MessageProtectionOrder>
- <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>
- <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>
- [方法: SecurityBindingElement を使用してカスタム バインドを作成する](how-to-create-a-custom-binding-using-the-securitybindingelement.md)
- [ユーザー定義バインディングの作成](../extending/creating-user-defined-bindings.md)
- [方法: 指定した認証モード用の SecurityBindingElement を作成する](how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)
