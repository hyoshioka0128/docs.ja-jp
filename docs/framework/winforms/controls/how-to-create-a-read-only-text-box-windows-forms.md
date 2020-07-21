---
title: '方法: 読み取り専用テキスト ボックスを作成する'
description: 編集可能な Windows フォームテキストボックスを読み取り専用の Windows フォームテキストボックスに変換する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- TextBox control [Windows Forms], read-only
- read-only text boxes
- text boxes [Windows Forms], read-only
ms.assetid: 60baa9ab-fa57-44ad-bb7c-61b05aa64296
ms.openlocfilehash: 5baa7c66d5f16560a4ea23861d563b099592957f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619365"
---
# <a name="how-to-create-a-read-only-text-box-windows-forms"></a>方法 : 読み取り専用テキスト ボックスを作成する (Windows フォーム)

編集可能な Windows フォームテキストボックスを読み取り専用のコントロールに変換できます。 たとえば、テキストボックスには通常は編集されているが、現在はアプリケーションの状態によっては編集されていない値が表示される場合があります。

## <a name="to-create-a-read-only-text-box"></a>読み取り専用のテキストボックスを作成するには

1. <xref:System.Windows.Forms.TextBox>コントロールの <xref:System.Windows.Forms.TextBoxBase.ReadOnly%2A> プロパティをに設定し `true` ます。 プロパティがに設定されている `true` 場合でも、ユーザーはテキストボックス内のテキストをスクロールして強調表示することができ、変更は許可されません。 **Copy**コマンドはテキストボックスで機能しますが、**切り取り**と**貼り付け**のコマンドは機能しません。

    > [!NOTE]
    > プロパティは、実行時の <xref:System.Windows.Forms.TextBoxBase.ReadOnly%2A> ユーザーの操作にのみ影響します。 テキストボックスの内容は、テキストボックスのプロパティを変更することで、実行時にプログラムによって変更することもでき <xref:System.Windows.Forms.TextBox.Text%2A> ます。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.TextBox>
- [TextBox コントロールの概要](textbox-control-overview-windows-forms.md)
- [方法: Windows フォーム TextBox コントロールでのカーソル位置を制御する](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [方法: Windows フォームの TextBox コントロールを使用してパスワード テキスト ボックスを作成する](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [方法: 文字列に引用符を挿入する](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [方法: Windows フォーム TextBox コントロールでテキストを選択する](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [方法: Windows フォーム TextBox コントロールで複数行を表示する](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox コントロール](textbox-control-windows-forms.md)
