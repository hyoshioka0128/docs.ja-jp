---
title: '方法: テキストのトリミングを有効にする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [WPF], trimming
- documents [WPF], trimming text
- trimming text [WPF]
ms.assetid: dd8c9191-d2be-45fd-9fb4-3c75b65578c5
ms.openlocfilehash: 25fff566868e792004a915fee195485c4a1f385f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776131"
---
# <a name="how-to-enable-text-trimming"></a>方法: テキストのトリミングを有効にする

この例では、<xref:System.Windows.TextTrimming> 列挙型で使用可能な値の使用方法と効果を示します。

## <a name="example"></a>例

次の例では、<xref:System.Windows.Controls.TextBlock.TextTrimming%2A> 属性セットを使用して <xref:System.Windows.Controls.TextBlock> 要素を定義します。

[!code-xaml[TextTrimmingSnippets#_TextTrimmingXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml#_texttrimmingxaml)]

コード内で対応する <xref:System.Windows.TextTrimming> プロパティを設定する方法を以下に示します。

[!code-csharp[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](~/samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml.cs#_texttrimmingsettexttrimming)]
[!code-vb[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextTrimmingSnippets/VisualBasic/Window1.xaml.vb#_texttrimmingsettexttrimming)]

現在、テキストのトリミングには次の 3 つのオプションがあります: **CharacterEllipsis**、**WordEllipsis**、**None**。

<xref:System.Windows.Controls.TextBlock.TextTrimming%2A> を **CharacterEllipsis** に設定した場合、テキストがトリミングされ、トリミング エッジに最も近い文字の位置に省略記号が続きます。  この設定では、トリミング境界により近い位置でテキストが切り取られます。ただし、単語の一部が切り取られる可能性があります。  次の図は、上記で定義したものと同様の <xref:System.Windows.Controls.TextBlock> におけるこの設定の効果を示しています。

![例:TextTrimming.CharacterEllipsis](./media/texttrimming-character.png "TextTrimming_Character")

<xref:System.Windows.Controls.TextBlock.TextTrimming%2A> を **WordEllipsis** に設定した場合、テキストがトリミングされ、トリミング エッジに最も近い位置にある最初の完全な単語の後に省略記号が続きます。  この設定では、部分的にトリミングされた単語は表示されませんが、**CharacterEllipsis** 設定よりもトリミング エッジから離れた位置でテキストがトリミングされる傾向にあります。  次の図は、上記で定義された <xref:System.Windows.Controls.TextBlock> のこの設定の効果を示しています。

![例:TextTrimming.WordEllipsis](./media/texttrimming-word.png "TextTrimming_Word")

<xref:System.Windows.Controls.TextBlock.TextTrimming%2A> が **None** に設定されている場合、テキストのトリミングは実行されません。  この場合、テキストは親テキスト コンテナーの境界にトリミングされるだけです。  次の図は、上記で定義したものと同様の <xref:System.Windows.Controls.TextBlock> におけるこの設定の効果を示しています。

![例:TextTrimming.None](./media/texttrimming-none.png "TextTrimming_None")
