---
ms.openlocfilehash: b6cb7edcd6bed50efdf59f3321320ac8cd1b1ab8
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617225"
---
### <a name="some-workflow-drag-and-drop-apis-are-obsolete"></a>一部の WorkFlow ドラッグ アンド ドロップ API が廃止されました

#### <a name="details"></a>説明

この WorkFlow ドラッグ アンド ドロップ API は廃止され、アプリが 4.5 向けにリビルドされた場合、コンパイラ警告が発生します。

#### <a name="suggestion"></a>提案される解決策

複数オブジェクトでの操作をサポートする新しい <xref:System.Activities.Presentation.DragDropHelper?displayProperty=fullName> API を代わりに使用する必要があります。 または、ビルド警告を抑制するか、古いコンパイラを使用して警告を回避できます。 API は、まだサポートされています。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Activities.Presentation.DragDropHelper.DoDragMove(System.Activities.Presentation.WorkflowViewElement,System.Windows.Point)?displayProperty=nameWithType>
- <xref:System.Activities.Presentation.DragDropHelper.GetCompositeView(System.Windows.DragEventArgs)?displayProperty=nameWithType>
- <xref:System.Activities.Presentation.DragDropHelper.GetDraggedModelItem(System.Windows.DragEventArgs)?displayProperty=nameWithType>
- <xref:System.Activities.Presentation.DragDropHelper.GetDroppedObject(System.Windows.DependencyObject,System.Windows.DragEventArgs,System.Activities.Presentation.EditingContext)?displayProperty=nameWithType>
