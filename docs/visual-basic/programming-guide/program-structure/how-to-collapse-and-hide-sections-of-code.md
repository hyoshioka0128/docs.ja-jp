---
title: '方法: コードのセクションを折りたたんで非表示にする'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic, code collapsing
- Visual Basic, code hiding
- Visual Basic code, collapsing and hiding
ms.assetid: b770e8f5-e07d-491a-ab4b-a977980f9ba2
ms.openlocfilehash: c11affe9c4dd4251ba8ff4b87029d314970b5fcb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404850"
---
# <a name="how-to-collapse-and-hide-sections-of-code-visual-basic"></a>方法: コードのセクションを折りたたんで非表示にする (Visual Basic)

`#Region` ディレクティブを使用すると、Visual Basic ファイル内のコードのセクションを折りたたんで非表示にすることができます。 `#Region` ディレクティブでは、Visual Studio コード エディターを使用するときに展開および折りたたみが可能なコード ブロックを指定できます。 コードを選択的に非表示にする機能により、ファイルが管理しやすくなり、読みやすくなります。 詳細については、「[アウトライン](/visualstudio/ide/outlining)」を参照してください。

`#Region` ディレクティブでは、`#If...#End If` などのコード ブロック セマンティクスがサポートされています。 つまり、あるブロックで開始し、別のブロックで終了することはできません。開始と終了は同じブロック内である必要があります。 `#Region` ディレクティブは、関数内ではサポートされていません。

## <a name="to-collapse-and-hide-a-section-of-code"></a>コードのセクションを折りたたんで非表示にするには

次の例のように、`#Region` ステートメントと `#End Region` ステートメントの間にコードのセクションを配置します。

[!code-vb[VbVbalrConditionalComp#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#6)]

`#Region` ブロックは、コード ファイル内で何回も使用できます。そのため、ユーザーはプロシージャやクラスの独自のブロックを定義し、それらを折りたたむことができます。 `#Region` ブロックは、他の `#Region` ブロック内に入れ子にすることもできます。

> [!NOTE]
> コードを非表示にしても、コンパイルが妨げられることはなく、`#If...#End If` ステートメントには影響しません。

## <a name="see-also"></a>関連項目

- [条件付きコンパイル](conditional-compilation.md)
- [#Region ディレクティブ](../../language-reference/directives/region-directive.md)
- [#If...Then...#Else ディレクティブ](../../language-reference/directives/if-then-else-directives.md)
- [アウトライン](/visualstudio/ide/outlining)
