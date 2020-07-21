---
ms.openlocfilehash: 2e13268d4983af5d2fdd6d12b4d9e67d61d07f3d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622034"
---
### <a name="profiling-aspnet-mvc4-apps-can-lead-to-fatal-execution-engine-error"></a>ASP.Net MVC4 アプリのプロファイリングにより、致命的な実行エンジン エラーが発生する可能性がある

#### <a name="details"></a>説明

NGEN/プロファイル アセンブリを使用するプロファイラーにより、起動時にプロファイルされた ASP.NET MVC4 アプリケーションがクラッシュし、"致命的な実行エンジン例外" が示される場合があります。

#### <a name="suggestion"></a>提案される解決策

この問題は、.NET Framework 4.5.2 で修正されます。 プロファイラーは、イベント マスクで <code>COR_PRF_DISABLE_ALL_NGEN_IMAGES</code> を指定することで、この問題を回避することもできます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|
