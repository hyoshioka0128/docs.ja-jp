---
ms.openlocfilehash: 22b5abbe769733e8d5ca3e78dd9e6e13b2363737
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620310"
---
### <a name="opt-in-break-to-revert-from-different-45-sql-generation-to-simpler-40-sql-generation"></a>異なる 4.5 SQL 生成からより単純な 4.0 SQL 生成に戻す

#### <a name="details"></a>説明

最初に OrderBy を使用せずに JOIN ステートメントを生成し、制限操作への呼び出しを含むクエリで、より単純な SQL が生成されるようになりました。 .NET Framework 4.5 へのアップグレード後、これらのクエリは以前のバージョンよりも複雑な SQL を生成しました。

#### <a name="suggestion"></a>提案される解決策

既定では、この機能は無効です。 Entity Framework がパフォーマンスを低下させる追加の JOIN ステートメントを生成する場合は、アプリケーション構成 (app.config) ファイルの <code>&lt;appSettings&gt;</code> セクションへ次のエントリを追加してこの機能を有効にできます。<pre><code class="lang-xml">&lt;add key=&quot;EntityFramework_SimplifyLimitOperations&quot; value=&quot;true&quot; /&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |透明|
|バージョン|4.5.2|
|種類|ランタイム|
