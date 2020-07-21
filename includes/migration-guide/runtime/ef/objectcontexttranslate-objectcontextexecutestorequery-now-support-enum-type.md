---
ms.openlocfilehash: 6af8e97423c04abca25feb8d77ea9ab6e198a4f0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620330"
---
### <a name="objectcontexttranslate-and-objectcontextexecutestorequery-now-support-enum-type"></a>ObjectContext.Translate と ObjectContext.ExecuteStoreQuery で列挙型がサポートされるようになった

#### <a name="details"></a>説明

.NET Framework 4.0 では、<code>ObjectContext.Translate</code> および <code>ObjectContext.ExecuteStoreQuery</code> メソッドのジェネリック パラメーター <code>T</code> を列挙型にすることはできませんでした。 このシナリオがサポートされるようになりました。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.0 では、列挙型に対して Translate または ExecuteStoreQuery が呼び出された場合、"0" が返されました。 この動作が望ましい場合は、呼び出しを定数 0 (または同等の列挙型) に置き換えてください。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Data.Objects.ObjectContext.Translate%60%601(System.Data.Common.DbDataReader)?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.Translate%60%601(System.Data.Common.DbDataReader,System.String,System.Data.Objects.MergeOption)?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601(System.String,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601(System.String,System.String,System.Data.Objects.MergeOption,System.Object[])?displayProperty=nameWithType></li></ul>|
