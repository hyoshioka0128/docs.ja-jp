---
ms.openlocfilehash: 2aa6603e2ed77ffa94fbc6325cd5db50985bda6a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620415"
---
### <a name="previewlostkeyboardfocus-is-called-repeatedly-if-its-handler-shows-a-windows-forms-message-box"></a>PreviewLostKeyboardFocus は、そのハンドラーが Windows フォーム メッセージ ボックスを表示する場合、繰り返し呼び出される

#### <a name="details"></a>説明

.NET Framework 4.5 以降では、<xref:System.Windows.UIElement.PreviewLostKeyboardFocus> ハンドラーから <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=nameWithType> を呼び出すと、メッセージ ボックスが閉じられたとき、ハンドラーが再実行して、メッセージ ボックスの無限ループになる可能性があります。

#### <a name="suggestion"></a>提案される解決策

この問題を回避するには、2 つの方法があります。<ol><li><xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=nameWithType> の代わりに <xref:System.Windows.MessageBox.Show%2A?displayProperty=nameWithType> を呼び出すことによって回避できます。</li><li><xref:System.Windows.UIElement.LostKeyboardFocus> イベント ハンドラーから (<xref:System.Windows.UIElement.PreviewLostKeyboardFocus?displayProperty=fullName> イベント ハンドラーではなく) メッセージ ボックスを表示することによって回避できます。</li></ol>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.ContentElement.PreviewLostKeyboardFocus?displayProperty=nameWithType></li><li><xref:System.Windows.IInputElement.PreviewLostKeyboardFocus?displayProperty=nameWithType></li><li><xref:System.Windows.UIElement.PreviewLostKeyboardFocus?displayProperty=nameWithType></li><li><xref:System.Windows.UIElement3D.PreviewLostKeyboardFocus?displayProperty=nameWithType></li></ul>|
