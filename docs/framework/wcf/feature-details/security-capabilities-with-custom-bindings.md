---
title: カスタム バインディングを使用したセキュリティ機能
ms.date: 03/30/2017
ms.assetid: a2425679-484a-4e6c-9c98-7da7304f1516
ms.openlocfilehash: 48d17543f2b133c74bcfa82cfe1a2a0de28b1d01
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595194"
---
# <a name="security-capabilities-with-custom-bindings"></a>カスタム バインディングを使用したセキュリティ機能
一般的なセキュリティ タスクのほとんどは、システム指定のバインディングのいずれかを使用して実行できます。 ただし、より高度な制御が必要な場合は、以下のトピックで説明するように、<xref:System.ServiceModel.Channels.SecurityBindingElement> を使用してカスタム バインドを作成できます。 カスタムバインディングの詳細については、「[カスタムバインド](../extending/custom-bindings.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [SecurityBindingElement 認証モード](securitybindingelement-authentication-modes.md)  
 カスタム バインドで使用できる認証モードについて説明します。  
  
 [方法: SecurityBindingElement を使用してカスタム バインドを作成する](how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 セキュリティ要素を使用してカスタム バインディングを作成するための基本手順について説明します。  
  
 [方法: 指定した認証モード用の SecurityBindingElement を作成する](how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)  
 指定した認証モード用のセキュリティ要素を作成する方法について説明します。  
  
 [方法: WSFederationHttpBinding のセキュリティで保護されたセッションを無効にする](how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 フェデレーション サービスを作成する際に、セキュリティで保護されたセッションを無効にする方法について説明します。  
  
 [方法: メッセージ リプレイ検出を有効にする](how-to-enable-message-replay-detection.md)  
 リプレイ攻撃の発生を確認する方法について説明します。  
  
 [方法: サポート資格情報を作成する](how-to-create-a-supporting-credential.md)  
 必要な場合に、サービスにサポート資格情報を提供する方法について説明します。  
  
 [方法: 署名確認を設定する](how-to-set-up-a-signature-confirmation.md)  
 メッセージにデジタル署名する際に署名を確認する手順について説明します。  
  
 [方法: 時刻のずれの最大値を設定する](how-to-set-a-max-clock-skew.md)  
 サービスとクライアント間で許容される最大の時刻のずれを設定する方法について説明します。  
  
 [方法: デジタル署名の暗号化を無効にする](how-to-disable-encryption-of-digital-signatures.md)  
 デジタル署名の暗号化を無効にするとどのようなパフォーマンス上の利点があるかを説明します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>  
  
 [\<security>](../../configure-apps/file-schema/wcf/security-of-custombinding.md)  
  
## <a name="related-sections"></a>関連項目  
 [保護レベルの理解](../understanding-protection-level.md)  
  
 [サービスおよびクライアントのセキュリティ保護](securing-services-and-clients.md)  
  
## <a name="see-also"></a>関連項目

- [バインディングとセキュリティ](bindings-and-security.md)
- [セキュリティの概要](security-overview.md)
- [システム標準のバインディング](../system-provided-bindings.md)
