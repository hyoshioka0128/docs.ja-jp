---
ms.openlocfilehash: 9131c91b34f4c24653dea37ea39af6be6e072287
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620335"
---
### <a name="enumerableemptylttresultgt-always-returns-cached-instance"></a>Enumerable.Empty&lt;TResult&gt; は、常にキャッシュされたインスタンスを返します

#### <a name="details"></a>説明

.NET Framework 4.5 以降では、<xref:System.Linq.Enumerable.Empty%60%601> は、常にキャッシュされた内部インスタンス <xref:System.Collections.Generic.IEnumerable%601> を返します。以前は、<xref:System.Linq.Enumerable.Empty%60%601> は、API が呼び出された時点で空の <xref:System.Collections.Generic.IEnumerable%601> をキャッシュしました。つまり、<xref:System.Linq.Enumerable.Empty%60%601> が迅速かつ同時に呼び出されるような条件では、API の別の呼び出しに対して、型の別のインスタンスが返される可能性がありました。

#### <a name="suggestion"></a>提案される解決策

以前の動作は非確定的なため、コードがそれに依存している可能性は低いです。 ただし、ありそうにないことですが、空の列挙が比較され、ときには等しくないことが予期されている場合には、<xref:System.Linq.Enumerable.Empty%60%601> を使用する代わりに、明示的に空の配列を作成する (<code>new T[0]</code>) 必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Linq.Enumerable.Empty%60%601?displayProperty=nameWithType></li></ul>|
