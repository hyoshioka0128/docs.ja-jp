---
ms.openlocfilehash: 063e10b0310880af255793215a80a5529a5db0ff
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616107"
---
### <a name="dbparameterprecision-and-dbparameterscale-are-now-public-virtual-members"></a>DbParameter.Precision と DbParameter.Scale は、パブリック仮想メンバーになった

#### <a name="details"></a>説明

<xref:System.Data.Common.DbParameter.Precision> および <xref:System.Data.Common.DbParameter.Scale> はパブリック仮想プロパティとして実装されます。 これらは、対応する明示的なインターフェイス実装、<xref:System.Data.Common.DbParameter.System%23Data%23IDbDataParameter%23Precision> と <xref:System.Data.Common.DbParameter.System%23Data%23IDbDataParameter%23Scale> を置き換えます。

#### <a name="suggestion"></a>提案される解決策

ADO.NET データベース プロバイダーを再構築するとき、これらの違いにより、「override」キーワードが Precision および Scale プロパティに適用される必要があります。 これは、コンポーネントを再構築するときにのみ必要です。既存のバイナリは引き続き機能します。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Data.Common.DbParameter.Precision?displayProperty=nameWithType>
- <xref:System.Data.Common.DbParameter.Scale?displayProperty=nameWithType>
