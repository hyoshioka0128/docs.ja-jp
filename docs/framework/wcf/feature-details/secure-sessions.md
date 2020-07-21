---
title: セキュリティで保護されたセッション
ms.date: 03/30/2017
ms.assetid: 7b50602f-d7b5-42e9-8e92-1f0413df0d8b
ms.openlocfilehash: cb02adc7514e27175088e7664b12e45bc8ca5cd9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84590086"
---
# <a name="secure-sessions"></a>セキュリティで保護されたセッション
Windows Communication Foundation (WCF) の機能は、メッセージが送信された順序で受信されることを保証する信頼できるセッションです。 このセクションの各トピックでは、信頼できるセッションを作成する際に考慮する必要のあるセキュリティへの影響について説明します。 信頼できるセッションの詳細については、「[セッションの使用](../using-sessions.md)」を参照してください。  
  
> [!NOTE]
> Windows XP で偽装が必要な場合は、ステートフルなセキュリティ コンテキスト トークン (SCT: Security Context Token) を使用しない、セキュリティで保護されたセッションを使用します。 ステートフル SCT が偽装と共に使用されると、<xref:System.InvalidOperationException> がスローされます。 詳細については、「サポートされ[ないシナリオ](unsupported-scenarios.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|||  
|-|-|  
|[セキュリティ保護されたメッセージ交換とセッション](secure-conversations-and-secure-sessions.md)|セキュリティで保護されたメッセージ交換とセキュリティで保護されたセッションは、同じ意味で使用されます。 ここでは、セキュリティで保護されたメッセージ交換のしくみ、およびこのパターンを使用する状況と理由について説明します。|  
|[方法: セキュリティで保護されたセッションを作成する](how-to-create-a-secure-session.md)|セキュリティで保護されたセッションの基本的な作成手順を説明するチュートリアルです。|  
|[方法: セキュリティで保護されたセッションに対しセキュリティ コンテキスト トークンを作成する](how-to-create-a-security-context-token-for-a-secure-session.md)|クライアントの状態とセッションを保持する Web ファームを作成する手順について説明します。|  
|[セキュリティで保護されたセッションに関するセキュリティの検討](security-considerations-for-secure-sessions.md)|セキュリティで保護されたセッションに関する特別な考慮事項について説明します。|  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
## <a name="related-sections"></a>関連項目  
 [セッション、インスタンス化、およびコンカレンシー](sessions-instancing-and-concurrency.md)  
  
 [サービスの設計と実装](../designing-and-implementing-services.md)  
  
## <a name="see-also"></a>関連項目

- [方法: メッセージ リプレイ検出を有効にする](how-to-enable-message-replay-detection.md)
- [リプレイ攻撃](replay-attacks.md)
- [方法: セッションを必要とするサービスを作成する](how-to-create-a-service-that-requires-sessions.md)
