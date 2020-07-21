---
title: '方法: デザイン時に Windows フォームのコントロールにツールヒントを設定する'
description: プログラムによって、または Visual Studio の Windows フォームデザイナーで、コントロールのツールヒントを設定する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tooltips [Windows Forms], for controls
- examples [Windows Forms], tooltips
ms.assetid: c4b60637-4c0a-44c2-a103-f66dff887936
ms.openlocfilehash: 144ba5b6bffb4a538e345f7b2df4a453fc6fd63d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618026"
---
# <a name="how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time"></a>方法: デザイン時に Windows フォームのコントロールにツールヒントを設定する

<xref:System.Windows.Forms.ToolTip>コードまたは Visual Studio の Windows フォームデザイナーで文字列を設定できます。 コンポーネントの詳細については <xref:System.Windows.Forms.ToolTip> 、「[ツールヒントコンポーネントの概要](tooltip-component-overview-windows-forms.md)」を参照してください。

## <a name="set-a-tooltip-programmatically"></a>プログラムによるツールヒントの設定

1. ツールヒントを表示するコントロールを追加します。

2. <xref:System.Windows.Forms.ToolTip.SetToolTip%2A>コンポーネントのメソッドを使用し <xref:System.Windows.Forms.ToolTip> ます。

    ```vb
    ' In this example, Button1 is the control to display the ToolTip.
    ToolTip1.SetToolTip(Button1, "Save changes")
    ```

    ```csharp
    // In this example, button1 is the control to display the ToolTip.
    toolTip1.SetToolTip(button1, "Save changes");
    ```

    ```cpp
    // In this example, button1 is the control to display the ToolTip.
    toolTip1->SetToolTip(button1, "Save changes");
    ```

## <a name="set-a-tooltip-in-the-designer"></a>デザイナーでのツールヒントの設定

1. Visual Studio で、コンポーネントを <xref:System.Windows.Forms.ToolTip> フォームに追加します。

2. ツールヒントを表示するコントロールを選択するか、フォームに追加します。

3. [**プロパティ**] ウィンドウで、ToolTip1 Value の**ツールヒント**を適切なテキスト文字列に設定します。

### <a name="to-remove-a-tooltip-programmatically"></a>プログラムによってツールヒントを削除するには

1. <xref:System.Windows.Forms.ToolTip.SetToolTip%2A>コンポーネントのメソッドを使用し <xref:System.Windows.Forms.ToolTip> ます。

    ```vb
    ' In this example, Button1 is the control displaying the ToolTip.
    ToolTip1.SetToolTip(Button1, Nothing)
    ```

    ```csharp
    // In this example, button1 is the control displaying the ToolTip.
    toolTip1.SetToolTip(button1, null);
    ```

    ```cpp
    // In this example, button1 is the control displaying the ToolTip.
    toolTip1->SetToolTip(button1, NULL);
    ```

## <a name="remove-a-tooltip-in-the-designer"></a>デザイナーのツールヒントを削除する

1. Visual Studio で、ツールヒントを表示しているコントロールを選択します。

2. [**プロパティ**] ウィンドウで、 **ToolTip1 のツールヒント**のテキストを削除します。

## <a name="see-also"></a>関連項目

- [ToolTip コンポーネントの概要](tooltip-component-overview-windows-forms.md)
- [方法: Windows フォームの ToolTip コンポーネントの遅延時間を変更する](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)
- [ToolTip コンポーネント](tooltip-component-windows-forms.md)
