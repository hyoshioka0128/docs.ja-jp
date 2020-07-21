---
title: 方法:テキストの文字体裁を変更する
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- setting Typography attributes [WPF]
- Typography attribute [WPF], setting
ms.assetid: 19a3b49b-60a2-4c11-a786-e26b4c965588
ms.openlocfilehash: 4c027424632f8671ba8d7cae1c899ef3a53edc26
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777027"
---
# <a name="how-to-alter-the-typography-of-text"></a>方法:テキストの文字体裁を変更する
次の例では、<xref:System.Windows.Documents.Paragraph> を例の要素として使用して、<xref:System.Windows.Documents.TextElement.Typography%2A> 属性を設定する方法を示しています。  
  
## <a name="example"></a>例  
 [!code-xaml[TextElementSnippets#_TextElement_TypogXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml#_textelement_typogxaml)]  
  
 この例の表示結果を次の図に示します。  
  
 ![スクリーンショット:文字体裁に変更があるテキスト](./media/textelement-typog.png "TextElement_Typog")  
  
 これに対し、既定の文字体裁プロパティを設定した同様の例がどのように表示されるかを次の図に示します。  
  
 ![スクリーンショット:文字体裁に変更があるテキスト](./media/textelement-typog-default.png "TextElement_Typog_Default")  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Controls.TextBox.Typography%2A> プロパティをプログラムで設定する方法を示しています。  
  
 [!code-csharp[TextElementSnippets#_TextElement_Typog](~/samples/snippets/csharp/VS_Snippets_Wpf/TextElementSnippets/CSharp/Window1.xaml.cs#_textelement_typog)]
 [!code-vb[TextElementSnippets#_TextElement_Typog](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextElementSnippets/visualbasic/window1.xaml.vb#_textelement_typog)]  
  
## <a name="see-also"></a>関連項目

- [フロー ドキュメントの概要](flow-document-overview.md)
