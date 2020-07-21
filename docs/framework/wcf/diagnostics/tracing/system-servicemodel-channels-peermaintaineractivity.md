---
title: System.ServiceModel.Channels.PeerMaintainerActivity
ms.date: 03/30/2017
ms.assetid: ef28d086-d7fb-4e81-82e9-45a54647783b
ms.openlocfilehash: ce97eaa2ad5c9dbd5f4d6f81186960c489eb4b85
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596078"
---
# <a name="systemservicemodelchannelspeermaintaineractivity"></a>System.ServiceModel.Channels.PeerMaintainerActivity
PeerMaintainer モジュールは、特定の操作を実行しています (詳細はトレース メッセージの本文に含まれています)。  
  
## <a name="description"></a>説明  
 このトレースは、各種の PeerMaintainer 操作中に行われます。  
  
 PeerMaintainer は PeerNode の内部コンポーネントです。 このコンポーネントは、毎分または 32 通のメッセージを受信するたびに近隣ノードに LinkUtility メッセージを送信します。このとき、交換されたメッセージ数と、有効な (重複および改ざんされていない) メッセージの数に関する統計が一緒に送信されます。 これは、特定の近隣ノードのリンク ユーティリティの特定に役立ちます。 約 5 分ごとに、保守管理者は近隣ノードの接続が正常かどうかを確認します。 近隣ノードへの接続数が適切な数を超えている場合、保守管理者は使用頻度が最も少ない接続を削除します。 接続数が十分でなければ、保守管理者は新しい接続を取得します。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
