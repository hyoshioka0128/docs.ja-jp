---
title: TextBox コントロールで複数の行を表示する
description: 複数行を表示する方法については、Windows フォームテキストボックスコントロールで複数行、ワードラップ、およびスクロールバーの各プロパティを設定する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- newline
- end of line
- ScrollBars property [Windows Forms], in TextBox control
- CRLF
- MultiLine property in TextBox control
- line-feed
- TextBox control [Windows Forms], viewing multiple lines
- carriage return
ms.assetid: 43173201-0b74-4067-a472-605029ca5f35
ms.openlocfilehash: e40d720bcd56366f4f06bfe2e2d347aaf9aa9d6c
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174472"
---
# <a name="how-to-view-multiple-lines-in-the-windows-forms-textbox-control"></a>方法: Windows フォーム TextBox コントロールで複数行を表示する
既定では、Windows フォーム <xref:System.Windows.Forms.TextBox> コントロールには1行のテキストが表示され、スクロールバーは表示されません。 テキストが使用可能な領域を超えている場合は、テキストの一部だけが表示されます。 この既定の動作を変更するには <xref:System.Windows.Forms.TextBox.Multiline%2A> 、、 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 、およびの <xref:System.Windows.Forms.TextBox.ScrollBars%2A> 各プロパティを適切な値に設定します。  
  
### <a name="to-display-a-carriage-return-in-the-textbox-control"></a>TextBox コントロールに復帰を表示するには  
  
- 複数行で復帰を表示するには、 <xref:System.Windows.Forms.TextBox> プロパティを使用し <xref:System.Environment.NewLine%2A> ます。  
  
     エスケープ文字 () の解釈は言語固有であることに注意して \\ ください。 Visual Basic は `Chr$(13) & Chr$(10)` 、キャリッジリターンとラインフィード文字の組み合わせにを使用します。  
  
### <a name="to-view-multiple-lines-in-the-textbox-control"></a>TextBox コントロールで複数の行を表示するには  
  
1. <xref:System.Windows.Forms.TextBox.Multiline%2A> プロパティを `true`に設定します。 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A>が `true` (既定値) の場合、コントロールのテキストは1つ以上の段落として表示されます。それ以外の場合は、コントロールの端で一部の行がクリップされる可能性があるリストとして表示されます。  
  
2. <xref:System.Windows.Forms.TextBox.ScrollBars%2A> プロパティに適切な値を設定します。  
  
    |値|説明|  
    |-----------|-----------------|  
    |<xref:System.Windows.Forms.ScrollBars.None>|この値は、ほとんど常にコントロールに収まらない段落の場合に使用します。 テキストが長すぎて一度に表示できない場合、ユーザーはマウスポインターを使用してコントロール内を移動できます。|  
    |<xref:System.Windows.Forms.ScrollBars.Horizontal>|この値は、行の一覧を表示する場合に使用します。その中には、コントロールの幅よりも長い場合があり <xref:System.Windows.Forms.TextBox> ます。|  
    |<xref:System.Windows.Forms.ScrollBars.Both>|リストがコントロールの高さよりも長い場合は、この値を使用します。|  
  
3. <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> プロパティに適切な値を設定します。  
  
    |値|説明|  
    |-----------|-----------------|  
    |`false`|コントロール内のテキストは自動的に折り返されないため、改行に達するまで右にスクロールします。 <xref:System.Windows.Forms.ScrollBars.Horizontal>上のスクロールバーまたはを選択した場合は、この値を使用し <xref:System.Windows.Forms.ScrollBars.Both> ます。|  
    |`true` (既定値)|水平スクロールバーは表示されません。 <xref:System.Windows.Forms.ScrollBars.Vertical>1 つ以上の段落を表示する場合は、この値を使用し <xref:System.Windows.Forms.ScrollBars.None> ます。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.TextBox>
- [TextBox コントロールの概要](textbox-control-overview-windows-forms.md)
- [方法: Windows フォーム TextBox コントロールでのカーソル位置を制御する](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [方法: Windows フォームの TextBox コントロールを使用してパスワード テキスト ボックスを作成する](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [方法: 読み取り専用テキスト ボックスを作成する](how-to-create-a-read-only-text-box-windows-forms.md)
- [方法: 文字列に引用符を挿入する](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [方法: Windows フォーム TextBox コントロールでテキストを選択する](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [TextBox コントロール](textbox-control-windows-forms.md)
