---
title: '方法: プログラムでテキストに要素を挿入する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Text Animation sample [WPF]
- elements [WPF], inserting into text
- inserting elements into text [WPF]
- TextPointer objects [WPF]
- text [WPF], inserting elements
ms.assetid: 97bd950a-25ac-4e42-a311-94b6420d4136
ms.openlocfilehash: ea9850c8490ec37032d4565c6b3375e3116d4313
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757116"
---
# <a name="how-to-insert-an-element-into-text-programmatically"></a>方法: プログラムでテキストに要素を挿入する
次の例では、<xref:System.Windows.Documents.TextPointer> オブジェクトを 2 つ使用し、<xref:System.Windows.Documents.Span> 要素の適用対象とする範囲をテキスト内で指定する方法を示します。  
  
## <a name="example"></a>例  
 [!code-csharp[FlowMiscSnippets_procedural_snip#InsertInlineIntoTextExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowMiscSnippets_procedural_snip/CSharp/InsertInlineIntoTextExample.cs#insertinlineintotextexamplewholepage)]
 [!code-vb[FlowMiscSnippets_procedural_snip#InsertInlineIntoTextExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowMiscSnippets_procedural_snip/VisualBasic/InsertInlineIntoTextExample.vb#insertinlineintotextexamplewholepage)]  
  
 次の図は、この例の結果を示したものです。  
  
 ![テキストの範囲に適用される Span 要素](./media/flow-insertelementintotextprogrammatically.png "Flow_InsertElementIntoTextProgrammatically")  
  
## <a name="see-also"></a>関連項目

- [フロー ドキュメントの概要](flow-document-overview.md)
