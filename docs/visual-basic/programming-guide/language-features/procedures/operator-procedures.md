---
title: 演算子プロシージャ
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], operator
- Visual Basic code, operators
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- overloaded operators [Visual Basic]
- operator overloading
- operator procedures
ms.assetid: 8c513d38-246b-4fb7-8b75-29e1364e555b
ms.openlocfilehash: a1dd183570c8aa50efff85bdaebef90bd3b0120f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364319"
---
# <a name="operator-procedures-visual-basic"></a>演算子プロシージャ (Visual Basic)

演算子プロシージャは、定義済みのクラスまたは構造体での標準演算子 (`*`、`<>`、`And` など) の動作を定義する一連の Visual Basic ステートメントです。 これは、"*演算子のオーバーロード*" とも呼ばれます。

## <a name="when-to-define-operator-procedures"></a>演算子プロシージャを定義する場合

クラスまたは構造体を定義したら、そのクラスまたは構造体の型で変数を宣言できます。 このような変数は、式の一部として演算に関与することが必要な場合があります。 そのためには、演算子のオペランドである必要があります。

Visual Basic では、基本的なデータ型でのみ演算子を定義します。 オペランドの一方または両方がクラスまたは構造体の型である場合、演算子の動作を定義できます。

詳細については、「[Operator Statement](../../../language-reference/statements/operator-statement.md)」をご覧ください。

## <a name="types-of-operator-procedure"></a>演算子プロシージャの型

演算子プロシージャは、次のいずれかの型にすることができます。

- 引数がクラスまたは構造体の型である単項演算子の定義。

- 引数の少なくとも 1 つがクラスまたは構造体の型である 2 項演算子の定義。

- 引数がクラスまたは構造体の型である変換演算子の定義。

- クラスまたは構造体の型を返す変換演算子の定義。

 変換演算子は常に単項であり、定義する演算子として常に `CType` を使用します。

## <a name="declaration-syntax"></a>宣言の構文

演算子プロシージャを宣言するための構文は次のとおりです。

```vb
Public Shared [Widening | Narrowing] Operator operatorsymbol ( operand1 [,  operand2 ]) As datatype

' Statements of the operator procedure.

End Operator
```

`Widening` または `Narrowing` キーワードは、型変換演算子でのみ使用します。 型変換演算子では、演算子記号は常に [CType 関数](../../../language-reference/functions/ctype-function.md)です。

2 項演算子を定義するには、2 つのオペランドを宣言し、型変換演算子を含め、単項演算子を定義するには、1 つのオペランドを宣言します。 すべてのオペランドを `ByVal` で宣言する必要があります。

[Sub プロシージャ](./sub-procedures.md)のパラメーターを宣言する場合と同様に、各オペランドを宣言します。

### <a name="data-type"></a>データの種類

定義済みのクラスまたは構造体で演算子を定義するため、オペランドの少なくとも一方は、そのクラスまたは構造体のデータ型である必要があります。 型変換演算子の場合、オペランドまたは戻り値の型が、クラスまたは構造体のデータ型である必要があります。

詳細については、「[Operator Statement](../../../language-reference/statements/operator-statement.md)」をご覧ください。

## <a name="calling-syntax"></a>呼び出しの構文

演算子プロシージャは、式で演算子記号を使用して暗黙的に呼び出します。 事前定義された演算子の場合と同様にオペランドを指定します。

演算子プロシージャの暗黙的な呼び出しの構文は次のとおりです。

`Dim testStruct As`  *構造体名*

`Dim testNewStruct As`  *構造体名*  `= testStruct`  *演算子記号*  `10`

### <a name="illustration-of-declaration-and-call"></a>宣言と呼び出しの実例

次の構造体は、構成要素の上位および下位の要素として、符号付き 128 ビット整数値を格納します。 2 つの `veryLong` 値を加算し、結果の `veryLong` 値を生成する `+` 演算子を定義します。

[!code-vb[VbVbcnProcedures#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#23)]

次の例は、`veryLong` で定義された `+` 演算子の一般的な呼び出しを示しています。

[!code-vb[VbVbcnProcedures#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#24)]

## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [Sub プロシージャ](./sub-procedures.md)
- [Function プロシージャ](./function-procedures.md)
- [Property プロシージャ](./property-procedures.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [Operator ステートメント](../../../language-reference/statements/operator-statement.md)
- [方法: 演算子を定義する](./how-to-define-an-operator.md)
- [方法: 変換演算子を定義する](./how-to-define-a-conversion-operator.md)
- [方法: 演算子プロシージャを呼び出す](./how-to-call-an-operator-procedure.md)
- [方法: 演算子を定義するクラスを使用する](./how-to-use-a-class-that-defines-operators.md)
