---
title: '#If...Then...#Else ディレクティブ'
ms.date: 04/11/2018
f1_keywords:
- vb.#EndIf
- '#End If'
- '#Then'
- '#ElseIf'
- vb.#ElseIf
- vb.#Else
- vb.#If
helpviewer_keywords:
- Visual Basic code, compiling
- '#If directive [Visual Basic]'
- conditional compilation [Visual Basic], directives
- '#End if directive [Visual Basic]'
- selective compiling
- else directive (#else)
- '#Else directive [Visual Basic]'
ms.assetid: 10bba104-e3fd-451b-b672-faa472530502
ms.openlocfilehash: 7054a6ada4583c5d89e020437eb622a59d3eb17a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410011"
---
# <a name="ifthenelse-directives"></a>#If...Then...#Else ディレクティブ

選択された Visual Basic コード ブロックを条件付きでコンパイルします。

## <a name="syntax"></a>構文

```vb
#If expression Then
   statements
[ #ElseIf expression Then
   [ statements ]
...
#ElseIf expression Then
   [ statements ] ]
[ #Else
   [ statements ] ]
#End If
```

## <a name="parts"></a>指定項目

`expression`  
`#If` および `#ElseIf` ステートメントでは必須、その他の場所では省略可能です。 1 つ以上の条件付きコンパイラ定数、リテラル、演算子のみで構成され、`True` または `False` に評価される式です。

`statements`  
`#If` ステートメント ブロックでは必須、その他の場所では省略可能です。 関連する式が `True` に評価された場合にコンパイルされる、Visual Basic のプログラム行またはコンパイラ ディレクティブです。

`#End If`  
`#If` ステートメント ブロックを終了します。

## <a name="remarks"></a>Remarks

表面上、`#If...Then...#Else` ディレクティブの動作は `If...Then...Else` ステートメントの動作と同じように見えます。 ただし、`#If...Then...#Else` ディレクティブではコンパイラによってコンパイルされる内容が評価されるのに対し、`If...Then...Else` ステートメントでは実行時に条件が評価されます。

通常、条件付きコンパイルは、異なるプラットフォームで同じプログラムをコンパイルする場合に使用されます。 また、デバッグ コードが実行可能ファイルに現れないようにするためにも使用されます。 条件付きコンパイルで除外されたコードは、最終的な実行可能ファイルから完全に削除されるため、サイズやパフォーマンスに影響しません。

評価の結果に関係なく、すべての式は `Option Compare Binary` を使用して評価されます。 `Option Compare` ステートメントは、`#If` および `#ElseIf` ステートメントの式には作用しません。

> [!NOTE]
> 1 行形式の `#If`、`#Else`、`#ElseIf`、`#End If` ディレクティブは存在しません。 この各ディレクティブと同じ行に他のコードを記述することはできません。

条件付きコンパイル ブロック内のステートメントは、完全な論理ステートメントでなければなりません。 たとえば、関数の属性のみを条件付きでコンパイルすることはできませんが、次のように関数をその属性ととも条件付きで宣言することはできます。

```vb
#If DEBUG Then
<WebMethod()>
Public Function SomeFunction() As String
#Else
<WebMethod(CacheDuration:=86400)>
Public Function SomeFunction() As String
#End If
```

## <a name="example"></a>例

この例では、`#If...Then...#Else` コンストラクトを使用して、特定のステートメントをコンパイルするかどうかを判断します。

[!code-vb[VbVbalrConditionalComp#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#1)]

## <a name="see-also"></a>関連項目

- [#Const ディレクティブ](const-directive.md)
- [If...Then...Else ステートメント](../statements/if-then-else-statement.md)
- [条件付きコンパイル](../../programming-guide/program-structure/conditional-compilation.md)
- <xref:System.Diagnostics.ConditionalAttribute?displayProperty=nameWithType>
