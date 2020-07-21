---
ms.openlocfilehash: 6da589057cebfbf3f67a46b8d49d3a61f037c4c7
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622257"
---
### <a name="crash-in-selector-when-removing-an-item-from-a-custom-incc-collection"></a>カスタム INCC コレクションから項目を削除すると、セレクターでクラッシュが発生する

#### <a name="details"></a>説明

<code>T:System.InvalidOperationException</code> は、次のシナリオで発生する可能性があります。<ul><li><code>T:System.Windows.Controls.Primitives.Selector</code> の ItemsSource が、<code>T:System.Collections.Specialized.INotifyCollectionChanged</code> のカスタム実装を含むコレクションである。</li><li>選択した項目をコレクションから削除する。</li><li><code>T:System.Collections.Specialized.NotifyCollectionChangedEventArgs</code> の <code>P:System.Collections.Specialized.NotifyCollectionChangedEventArgs.OldStartingIndex</code> が -1 (不明な位置を示す) である。</li></ul>例外のコールスタックは、System.Windows.Threading.Dispatcher.VerifyAccess()、System.Windows.DependencyObject.GetValue(DependencyProperty dp)、System.Windows.Controls.Primitives.Selector.GetIsSelected(DependencyObject element) で始まります。アプリケーションに複数のディスパッチャー スレッドがある場合、この例外は .NET Framework 4.5 で発生する可能性があります。 .NET Framework 4.7 では、1 つのディスパッチャー スレッドのアプリケーションでも例外が発生する場合があります。 この問題は .NET Framework 4.7.1 で修正されます。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.1 にアップグレードします。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.7|
|種類|ランタイム|
