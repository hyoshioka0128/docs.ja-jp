---
ms.openlocfilehash: 62702de022656e45466a45f4150e518226a3fecc
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621993"
---
### <a name="improvements-to-grid-star-rows-space-allocating-algorithm"></a>グリッド スター行領域の割り当てアルゴリズムの改善

#### <a name="details"></a>説明

.NET Framework 4.7 で導入された <xref:System.Windows.Controls.Grid> で[サイズを割り当てるためのアルゴリズム](https://github.com/Microsoft/dotnet/blob/master/Documentation/compatibility/wpf-grid-allocation-of-space-to-star-columns.md)) のバグを修正しました。  空の行を含む <code>Height=&quot;Auto&quot;</code> のグリッドなど、場合によっては、行が正しくない位置に配置され、すべてグリッドの外側に示されることがありました。

#### <a name="suggestion"></a>提案される解決策

アプリケーションでこれらの変更を利用するには、.NET Framework 4.8 以降で実行する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |Major|
|バージョン|4.8|
|種類|ランタイム|
