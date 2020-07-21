---
ms.openlocfilehash: f4ff938b2d0e9ead481fdf239aed8a6b918a99b0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620450"
---
### <a name="listboxitem-isselected-binding-issue-with-observablecollectionlttgtmove"></a>ObservableCollection&lt;T&gt;.Move に対する ListBoxItem IsSelected のバインディングの問題

#### <a name="details"></a>説明

項目が選択された <xref:System.Windows.Controls.ListBox?displayProperty=fullName> にバインドされるコレクションで <xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)> または <xref:System.Collections.ObjectModel.ObservableCollection%601.MoveItem(System.Int32,System.Int32)> を呼び出すと、<xref:System.Windows.Controls.ListBox?displayProperty=fullName> 項目の今後の選択または選択解除で不規則な動作が発生する可能性があります。

#### <a name="suggestion"></a>提案される解決策

<xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)> ではなく <xref:System.Collections.ObjectModel.Collection%601.Remove(%600)?displayProperty=fullName> と <xref:System.Collections.ObjectModel.Collection%601.Insert(System.Int32,%600)?displayProperty=fullName> を呼び出すことで、この問題は解決されます。 または、この問題は .NET Framework 4.6 で修正されたため、このバージョンの .NET Framework にアップグレードすることによって対処できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Collections.ObjectModel.ObservableCollection%601.MoveItem(System.Int32,System.Int32)?displayProperty=nameWithType></li></ul>|
