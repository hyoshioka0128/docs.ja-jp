---
ms.openlocfilehash: b521f4163bf5bf4a369d0eec12dae503703a976e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614648"
---
### <a name="throttle-concurrent-requests-per-session"></a>セッションあたりの同時実行される要求のスロットル

#### <a name="details"></a>説明

.NET Framework 4.6.2 以前の場合、ASP.NET は同じ Sessionid の要求を順番に実行します。ASP.NET は既定で常にクッキーを経由して Sessionid を発行します。 ページの応答に長い時間がかかる場合、ブラウザーの <kbd>F5</kbd> を押すだけで、サーバーのパフォーマンスが大幅に低下します。 この修正プログラムでは、キューに置かれた要求を追跡し、特定の制限を超えたときに要求を終了するためのカウンターを追加しました。 既定値は 50 です。 制限に達すると、警告がイベント ログに記録され、HTTP 500 応答は IIS ログに記録される可能性があります。

#### <a name="suggestion"></a>提案される解決策

以前の動作を復元するには、次の設定を web.config ファイルに追加して、新しい動作を無効にできます。

```xml
<appSettings>
    <add key="aspnet:RequestQueueLimitPerSession" value="2147483647"/>
</appSettings>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |
