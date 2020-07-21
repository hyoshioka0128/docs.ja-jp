---
ms.openlocfilehash: e0f72d19a884087b1f0f6ebd1b6baea75bc37af4
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620486"
---
### <a name="wpf-spawns-a-wisptisexe-process-which-can-freeze-the-mouse"></a>WPF が wisptis.exe プロセスを生成し、マウスがフリーズする可能性がある

#### <a name="details"></a>説明

この問題は 4.5.2 から発生するようになり、<code>wisptis.exe</code> が生成され、マウス入力がフリーズする可能性があります。

#### <a name="suggestion"></a>提案される解決策

この問題はサービス リリースの .NET Framework 4.5.2 (修正プログラム ロールアップ 3026376) で、あるいは .NET Framework 4.6 にアップグレードすることで解決できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |Major|
|バージョン|4.5.2|
|種類|ランタイム|
