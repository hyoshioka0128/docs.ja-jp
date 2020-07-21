---
title: '方法: Windows フォームを印刷する'
description: CopyFromScreen メソッドを使用して、現在の Windows フォームのコピーをプログラムで印刷する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms, printing
- printing [Windows Forms]
- printing a form
- printing [Windows Forms], printing a form
ms.assetid: c8dff5f8-f56a-4c07-ae31-64643b31f8fc
ms.openlocfilehash: b59ea4b5347903b36a166c4f8ac0d8d7db18635e
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174693"
---
# <a name="how-to-print-a-windows-form"></a>方法: Windows フォームを印刷する
開発プロセスの一環として、通常は Windows フォームのコピーを印刷します。 次のコード例は、メソッドを使用して、現在のフォームのコピーを印刷する方法を示して <xref:System.Drawing.Graphics.CopyFromScreen%2A> います。  
  
## <a name="example"></a>例  
 [!code-csharp[System.Drawing.Graphics.CopyFromScreen#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Graphics.CopyFromScreen/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.Graphics.CopyFromScreen#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Graphics.CopyFromScreen/VB/Form1.vb#1)]  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 次の条件を満たす場合は、例外が発生する可能性があります。  
  
- プリンターにアクセスするためのアクセス許可がありません。  
  
- プリンターがインストールされていません。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 このコード例を実行するには、コンピューターで使用するプリンターにアクセスするためのアクセス許可が必要です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Drawing.Printing.PrintDocument>
- [方法: GDI+ を使用してイメージをレンダリングする](how-to-render-images-with-gdi.md)
- [方法: Windows フォームでグラフィックスを印刷する](how-to-print-graphics-in-windows-forms.md)
