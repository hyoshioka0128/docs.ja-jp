---
title: オブジェクト変数
ms.date: 07/20/2015
helpviewer_keywords:
- object variables [Visual Basic], about object variables
- variables [Visual Basic], object
- objects [Visual Basic], accessing
- object variables [Visual Basic]
ms.assetid: 6169a196-2b13-4ba5-a205-154bc1b87844
ms.openlocfilehash: a5e61f9308d3484dc228a7d09cc2fd30a2f41b35
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410336"
---
# <a name="object-variables-in-visual-basic"></a>Visual Basic におけるオブジェクト変数

変数では、値を直接格納するだけでなく、オブジェクトを参照することもできます。 変数に任意の値を代入するのと同じ理由で、オブジェクトを変数に割り当てます。

- 変数名は大抵、オブジェクトそのものにアクセスするために必要なメソッドやプロパティの完全なパスよりも短く、覚えやすいものです。

- オブジェクトを参照する変数を使用する方が、必要なメソッドやプロパティを通じてオブジェクト自体に繰り返しアクセスするよりも効率的です。

- 変数を変更して、コードの実行中に他のオブジェクトを参照することができます。

## <a name="making-code-shorter"></a>コードを短くする

オブジェクト変数を使用すると、入力するコードを短くすることができます。 次の例では、メソッドとプロパティの完全なパスを使用して、<xref:System.Windows.Forms.Control> オブジェクトにアクセスします。

```vb
' Assume Me is a valid Form, or replace Me with a valid Form.
Me.ActiveForm.ActiveControl.Text = "Test"
Me.ActiveForm.ActiveControl.Location = New Point(100, 100)
Me.ActiveForm.ActiveControl.Show()
```

コントロールにオブジェクト変数を使用すると、このコードを短くして、実行速度を上げることができます。 オブジェクト変数は、割り当てる特定のクラス (この場合は `Control`) を使用して宣言する必要があります。 オブジェクトを変数に割り当てると、参照先のオブジェクトを扱う場合とまったく同じように扱うことができます。 オブジェクトのプロパティを設定または取得することも、そのメソッドのいずれかを使用することもできます。 次の例では、オブジェクト変数を使用して、前の例のコードを簡略化します。

```vb
Dim ctrlActv As System.Windows.Forms.Control = Me.ActiveForm.ActiveControl
ctrlActv.Text = "Test"
ctrlActv.Location = New Point(100, 100)
ctrlActv.Show()
```

## <a name="see-also"></a>関連項目

- [変数宣言](variable-declaration.md)
- [方法: 長い修飾パスを持つオブジェクトへのアクセス時間を短縮する](how-to-speed-up-access-to-an-object-with-a-long-qualification-path.md)
- [オブジェクト変数の宣言](object-variable-declaration.md)
- [オブジェクト変数の代入](object-variable-assignment.md)
- [オブジェクト変数の値](object-variable-values.md)
