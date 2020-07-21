---
ms.openlocfilehash: 5d5423d18091545ad9d50325900f5a9a4fff6dd9
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622013"
---
### <a name="fixed-a-hang-when-listbox-contains-duplicate-value-types"></a>ListBox に重複する値型が含まれている場合のハングの修正

#### <a name="details"></a>説明

Items コレクションに重複する値型オブジェクトが含まれていると、<xref:System.Windows.Controls.ItemsControl> の仮想化がスクロール中にハングする場合がある問題を修正しました。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |Major|
|バージョン|4.8|
|種類|ランタイム|
