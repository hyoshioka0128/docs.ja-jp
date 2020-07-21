---
title: '方法: キーボード入力をフォーム レベルで処理する'
description: メッセージがコントロールに到着する前に、Windows フォームのキーボード入力をフォームレベルで処理する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboard input [Windows Forms], at form level
- Windows Forms, handling keyboard input
- keyboards [Windows Forms], form-level input
ms.assetid: d7f8b390-dc91-42d2-ae0f-2ffa388127ad
ms.openlocfilehash: 6f0695b6f665a613e0e4e001a4f9bbfc09dd45ed
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904157"
---
# <a name="how-to-handle-keyboard-input-at-the-form-level"></a>方法: キーボード入力をフォーム レベルで処理する
Windows フォームでは、キーボード メッセージがコントロールに到達する前に、それらのメッセージをフォーム レベルで処理できます。 ここでは、このタスクを実行する方法について説明します。  
  
### <a name="to-handle-a-keyboard-message-at-the-form-level"></a>キーボード入力をフォーム レベルで処理するには  
  
- スタートアップ フォームの <xref:System.Windows.Forms.Control.KeyPress> イベントまたは <xref:System.Windows.Forms.Control.KeyDown> イベントを処理し、このフォームの <xref:System.Windows.Forms.Form.KeyPreview%2A> プロパティを `true` に設定して、キーボード メッセージがフォーム上のコントロールに到達する前にフォームによって受け取られるようにします。 次のコード例では、<xref:System.Windows.Forms.Control.KeyPress> イベントを処理して、すべての数値キーを検出し、"1"、"4"、および "7" の各キーを使用します。  
  
     [!code-cpp[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/cpp/form1.cpp#10)]
     [!code-csharp[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/CS/form1.cs#10)]
     [!code-vb[System.Windows.Forms.KeyboardInputForm#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/VB/form1.vb#10)]  
  
## <a name="example"></a>例  
 次のコード例は、上の例の完全なアプリケーションです。 このアプリケーションには、<xref:System.Windows.Forms.TextBox> の他に、<xref:System.Windows.Forms.TextBox> からフォーカスを移動できるようにするいくつかのコントロールが含まれています。 メイン <xref:System.Windows.Forms.Form> の <xref:System.Windows.Forms.Control.KeyPress> イベントは "1"、"4"、および "7" の各キーを使用し、<xref:System.Windows.Forms.TextBox> の <xref:System.Windows.Forms.Control.KeyPress> イベントは "2"、"5"、および "8" の各キーを使用します。残りのキーは表示されるだけです。 <xref:System.Windows.Forms.TextBox> にフォーカスがあるときに数値キーを押すと生成される <xref:System.Windows.Forms.MessageBox> 出力と、他のコントロールのいずれかにフォーカスがあるときに数値キーを押すと生成される <xref:System.Windows.Forms.MessageBox> 出力を比較してください。  
  
 [!code-cpp[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/cpp/form1.cpp#0)]
 [!code-csharp[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.KeyBoardInputForm#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInputForm/VB/form1.vb#0)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- System、System.Drawing、および System.Windows.Forms の各アセンブリへの参照。  
  
## <a name="see-also"></a>こちらもご覧ください

- [Windows フォーム アプリケーションにおけるキーボード入力](keyboard-input-in-a-windows-forms-application.md)
