---
title: 表記規則とコード規則
ms.date: 07/20/2015
helpviewer_keywords:
- coding conventions [Visual Basic], Visual Basic
- best practices [Visual Basic], coding conventions
- conventions [Visual Basic], Visual Basic coding
- typographic conventions [Visual Basic]
- document conventions [Visual Basic]
- conventions [Visual Basic], documentation
- Visual Basic code, conventions
ms.assetid: 1916cd81-ea9d-4faa-81f7-4a0d864b60f4
ms.openlocfilehash: 0e36d9d61b0dd2701210ce614d15fd38f08f5401
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401356"
---
# <a name="typographic-and-code-conventions-visual-basic"></a>表記規則とコード規則 (Visual Basic)

Visual Basic のドキュメントでは、次の表記規則とコード規則を使用します。  
  
## <a name="typographic-conventions"></a>表記規則  
  
|例|説明|  
|-------------|-----------------|  
|`Sub`, `If`, `ChDir`, `Print`, `True`, `Debug`|言語固有のキーワードとランタイム メンバーは、先頭文字が大文字であり、この例のように書式設定されます。|  
|**SmallProject**、**ButtonCollection**|入力を求められる語句は、この例のように書式設定されます。|  
|[Module ステートメント](statements/module-statement.md)|別のヘルプ ページにアクセスするためにクリックするリンクは、この例のように書式設定されます。|  
|*object*、*variableName*、`argumentList`|指定する情報のプレースホルダーは、この例のように書式設定されます。|  
|[ Shadows ]、[ *expressionList* ]|構文では、省略可能な項目は角かっこで囲まれています。|  
|{ `Public` &#124; `Friend` &#124; `Private` }|構文で、2 つ以上の項目のいずれかを選択する必要がある場合、項目は中かっこで囲まれ、縦棒で区切られます。<br /><br /> 項目を 1 つだけ選択する必要があります。|  
|[ `Protected` &#124; `Friend` ]|構文で、2 つ以上の項目から任意で選択できる場合、項目は角かっこで囲まれ、縦棒で区切られます。<br /><br /> 項目は自由に組み合わせて選択でき、項目をまったく選択しないこともできます。|  
|[{ `ByVal` &#124; `ByRef` }]|構文で、項目を 1 つのみ選択できるが、項目を完全に省略することもできる場合、これらの項目は、中かっこで囲まれて角かっこで囲まれ、縦棒で区切られます。|  
|*memberName*1、*memberName*2、*memberName*3|同じプレースホルダーの複数のインスタンスは、例に示すように、添字により区別されます。|  
|*memberName1*<br /><br /> ...<br /><br /> *memberNameN*|構文では、省略記号 (...) を使用して、省略記号の直前にある種類の項目の数が不定であることを示します。<br /><br /> コード内の省略記号は、わかりやすくするために省略されたコードを示します。|  
|ESC、ENTER|キーボードのキー名とキー シーケンスは、すべて大文字で表示されます。|  
|Alt + F1|各キー名の間にプラス記号 (+) が表示されている場合は、一方のキーを押しながらもう一方のキーを押す必要があります。 たとえば、ALT + F1 は、ALT キーを押しながら F1 キーを押すことを意味します。|  
  
## <a name="code-conventions"></a>コード規則  
  
|例|説明|  
|-------------|-----------------|  
|`sampleString = "Hello, world!"`|コード サンプルは固定ピッチ フォントで表示され、次の例のように書式設定されます。|  
|上記のステートメントは、`sampleString` の値を "Hello, world!" に設定します|次の例に示すように、説明文のコード要素は固定ピッチ フォントで表示されます。|  
|`' This is a comment.`<br /><br /> `REM This is also a comment.`|コードのコメントは、アポストロフィ (') または REM キーワードで始まります。|  
|`sampleVar = "This is an " _`<br /><br /> `& "example" _`<br /><br /> `& " of how to continue code."`|行の末尾にスペースに続いてアンダースコア (_) があるは、ステートメントが次の行に続くことを示します。|  
  
## <a name="see-also"></a>関連項目

- [Visual Basic の言語リファレンス](index.md)
- [キーワード](keywords/index.md)
- [Visual Basic ランタイム ライブラリのメンバー](runtime-library-members.md)
- [Visual Basic の名前付け規則](../programming-guide/program-structure/naming-conventions.md)
- [方法: コード内でステートメントを分割および連結する](../programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
- [コード内のコメント](../programming-guide/program-structure/comments-in-code.md)
