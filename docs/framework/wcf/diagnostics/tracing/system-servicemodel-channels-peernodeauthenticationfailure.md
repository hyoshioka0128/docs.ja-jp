---
title: System.ServiceModel.Channels.PeerNodeAuthenticationFailure
ms.date: 03/30/2017
ms.assetid: 0b50f782-ca06-4a82-aa7f-71f78ddc5177
ms.openlocfilehash: cb7019f1e4b47bde7c98b0109afa7b0125b7ef63
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84577306"
---
# <a name="systemservicemodelchannelspeernodeauthenticationfailure"></a>System.ServiceModel.Channels.PeerNodeAuthenticationFailure
潜在的な近隣ノードとのセキュリティ ハンドシェイクに失敗しました。  
  
## <a name="description"></a>説明  
 このトレースは、セキュリティで保護された近隣との接続を確立するときに行われます。 これは、資格情報が十分でないか間違っている場合に発生します。  
  
 PeerChannel では、トークンの種類として、強力な識別手段である X.509 証明書だけを認識します。X.509 証明書は、実装可能な認証および承認の種類に基づいて強力な ID モデルを提供します。 PeerChannel では、パスワードを使用した簡単なアプリケーションもサポートしています。 パスワードは、セッションへのエントリを許可する目的でのみ使用できます。パスワードを使用して、メッセージの認証を行うことはできません。 これは、ピア グループで共有する共通鍵トークンをソース認証に使用することは困難かつ不適切であるためです。  
  
## <a name="troubleshooting"></a>トラブルシューティング  
 すべての近隣ノードに適切なセキュリティ資格情報があることを確認します。  
  
## <a name="see-also"></a>関連項目

- [ピア チャネルのセキュリティ](../../feature-details/peer-channel-security.md)
- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
