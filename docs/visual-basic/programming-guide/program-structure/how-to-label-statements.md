---
title: '方法: ステートメントへのラベル付け'
ms.date: 07/20/2015
helpviewer_keywords:
- colons (:)
- statements [Visual Basic], labels
- ': separator character'
- Visual Basic code, labeling statements
ms.assetid: 38f1ff43-2054-42cb-963b-1998e60c6ed4
ms.openlocfilehash: 8f04d592c51b6a0630bfe623fd3574555aef9ff8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403214"
---
# <a name="how-to-label-statements-visual-basic"></a>方法: ステートメントにラベルを付ける (Visual Basic)

ステートメント ブロックは、コロンで区切られたコード行で構成されます。 行の前に識別文字列または整数が指定されたコード行は、"*ラベル付けされている*" といいます。 `On Error Goto` などのステートメントで使用するために、ステートメント ラベルでコード行をマークして識別します。

ラベルには、有効な Visual Basic 識別子 (プログラミング要素を識別するものなど) または整数リテラルを指定できます。 ラベルは、ソース コードの行の先頭に配置する必要があり、その後にコロンを指定する必要があります。同じ行でコロンの後にステートメントが続くかどうかは関係ありません。

コンパイラは、行の先頭が既に定義されている識別子と一致するかどうかをチェックすることでラベルを識別します。 一致しない場合、コンパイラはそれをラベルと見なします。

ラベルには独自の宣言領域があり、他の識別子に干渉することはありません。 ラベルのスコープはメソッドの本体です。 あいまいな状況では、ラベルの宣言が優先されます。

> [!NOTE]
> ラベルは、メソッド内の実行可能なステートメントでのみ使用できます。

## <a name="to-label-a-line-of-code"></a>コード行にラベルを付けるには

ソース コードの行の先頭に識別子を配置し、その後にコロンを配置します。

たとえば、次のコード行は、それぞれ `Jump` と `120` でラベル付けされています。

[!code-vb[VbVbalrStatements#708](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#708)]

## <a name="see-also"></a>関連項目

- [ステートメント](../language-features/statements.md)
- [宣言された要素の名前](../language-features/declared-elements/declared-element-names.md)
- [プログラム構造とコード規則](program-structure-and-code-conventions.md)
