---
title: Operator Statement
ms.date: 07/20/2015
f1_keywords:
- vb.operator
helpviewer_keywords:
- operators [Visual Basic]
- procedures [Visual Basic], operator
- Narrowing keyword [Visual Basic], conversion operators
- Visual Basic code, operators
- Widening keyword [Visual Basic], conversion operators
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- overloaded operators [Visual Basic]
- operator overloading
- operator procedures
- Operator statement [Visual Basic]
- CType function [Visual Basic], Operator statement
ms.assetid: b12ec4af-1ad7-4a17-865b-c5ee96320ae5
ms.openlocfilehash: f9e6ffe5a49715592399321ab471d73826e05d8e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404396"
---
# <a name="operator-statement"></a>Operator Statement

クラスまたは構造体に演算子プロシージャを定義する演算子シンボル、オペランド、およびコードを宣言します。

## <a name="syntax"></a>構文

```vb
[ <attrlist> ] Public [ Overloads ] Shared [ Shadows ] [ Widening | Narrowing ]
Operator operatorsymbol ( operand1 [, operand2 ]) [ As [ <attrlist> ] type ]
    [ statements ]
    [ statements ]
    Return returnvalue
    [ statements ]
End Operator
```

## <a name="parts"></a>指定項目

`attrlist`  
任意。 「[属性リスト](attribute-list.md)」を参照してください。

`Public`  
必須です。 この演算子プロシージャが [Public](../modifiers/public.md) アクセス権を持つことを示します。

`Overloads`  
任意。 「[Overloads](../modifiers/overloads.md)」を参照してください。

`Shared`  
必須です。 この演算子プロシージャが [Shared](../modifiers/shared.md)プロシージャであることを示します。

`Shadows`  
任意。 「[Shadows](../modifiers/shadows.md)」を参照してください。

`Widening`  
`Narrowing` を指定しない場合、変換演算子に必須です。 この演算子プロシージャでは、[拡大](../modifiers/widening.md)変換を定義していることを示します。 このヘルプページの「拡大変換と縮小変換」を参照してください。

`Narrowing`  
`Widening` を指定しない場合、変換演算子に必須です。 この演算子プロシージャでは、[縮小](../modifiers/narrowing.md)変換を定義していることを示します。 このヘルプページの「拡大変換と縮小変換」を参照してください。

`operatorsymbol`  
必須です。 この演算子プロシージャで定義する演算子のシンボルまたは識別子。

`operand1`  
必須です。 単項演算子 (変換演算子を含む) の 1 つのオペランドまたは二項演算子の左オペランドの名前と型。

`operand2`  
二項演算子に必須です。 二項演算子の右オペランドの名前と型。

`operand1` と `operand2` の構文と指定項目は次のとおりです。

`[ ByVal ] operandname [ As operandtype ]`

|パーツ|説明|
|----------|-----------------|
|`ByVal`|省略可能ですが、引渡し方法は [ByVal](../modifiers/byval.md) にする必要があります。|
|`operandname`|必須です。 このオペランドを表す変数の名前。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。|
|`operandtype`|`Option Strict` が `On` である場合を除き、省略可能です。 このオペランドのデータ型。|

`type`  
`Option Strict` が `On` である場合を除き、省略可能です。 演算子プロシージャで返される値のデータ型。

`statements`  
任意。 演算子プロシージャで実行されるステートメントのブロック。

`returnvalue`  
必須です。 演算子プロシージャから呼び出し元のコードに返される値。

`End` `Operator`  
必須です。 この演算子プロシージャの定義を終了します。

## <a name="remarks"></a>Remarks

`Operator` は、クラスまたは構造体でのみ使用できます。 つまり、演算子の*宣言コンテキスト*は、ソース ファイル、名前空間、モジュール、インターフェイス、プロシージャ、ブロックにすることができません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

すべての演算子は `Public Shared` である必要があります。 どのオペランドにも `ByRef`、`Optional`、`ParamArray` を指定することはできません。

戻り値を保持するために、演算子シンボルや識別子を使用することはできません。 `Return` ステートメントを使用する必要があり、それによって値を指定する必要があります。 任意の数の `Return` ステートメントをプロシージャ内の任意の場所に記述できます。

この方法で演算子を定義することは、`Overloads` キーワードを使用するかどうかにかかわらず、*演算子のオーバーロード*と呼ばれます。 定義可能な演算子を次の表に示します。

|種類|演算子|
|----------|---------------|
|単項|`+`, `-`, `IsFalse`, `IsTrue`, `Not`|
|2 項|`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`|
|変換 (単項)|`CType`|

2 項の一覧に示した `=` 演算子は比較演算子であり、代入演算子ではありません。

`CType` を定義する場合、`Widening` または `Narrowing` のどちらかを指定する必要があります。

## <a name="matched-pairs"></a>一致したペア

特定の演算子を一致したペアとして定義する必要があります。 そのようなペアのどちらかの演算子を定義する場合は、他方の演算子も定義する必要があります。 一致したペアは次のとおりです。

- `=` および `<>`

- `>` および `<`

- `>=` および `<=`

- `IsTrue` および `IsFalse`

## <a name="data-type-restrictions"></a>データ型の制限

定義するすべての演算子には、それを定義するクラスまたは構造体が関係している必要があります。 つまり、クラスまたは構造体が、次のデータ型として指定されている必要があります。

- 単項演算子のオペランド。

- 二項演算子の少なくとも 1 つのオペランド。

- 変換演算子のオペランドまたは戻り値の型。

 特定の演算子には、次のような追加のデータ型の制限があります。

- `IsTrue` 演算子と `IsFalse` 演算子を定義する場合、それらはどちらも `Boolean` 型を返す必要があります。

- `<<` 演算子と `>>` 演算子を定義する場合、それらはどちらも `operand2` の `operandtype` に `Integer` 型を指定する必要があります。

戻り値の型は、どちらかのオペランドの型に対応している必要はありません。 たとえば、`=` や `<>` などの比較演算子では、どちらのオペランドも `Boolean` でない場合でも `Boolean` を返すことができます。

## <a name="logical-and-bitwise-operators"></a>論理演算子とビット処理演算子

`And`、`Or`、`Not`、および `Xor` の各演算子では、Visual Basic で論理演算またはビットごとの演算を実行できます。 ただし、クラスまたは構造体でこれらの演算子のいずれかを定義した場合は、そのビットごとの演算のみを定義できます。

`Operator` ステートメントで、`AndAlso` 演算子を直接定義することはできません。 ただし、次の条件を満たしている場合は、`AndAlso` を使用できます。

- `AndAlso` に使用する同じオペランド型に対して `And` を定義している。

- `And` の定義で、それを定義したクラスまたは構造体と同じ型を返す。

- `And` を定義したクラスまたは構造体に `IsFalse` 演算子を定義している。

同様に、クラスまたは構造体の戻り値の型で同じオペランドに対して `Or` を定義し、クラスまたは構造体に `IsTrue` を定義している場合、`OrElse` を使用できます。

## <a name="widening-and-narrowing-conversions"></a>Widening and Narrowing Conversions

*拡大変換*は実行時に常に成功しますが、*縮小変換*は実行時に失敗する可能性があります。 詳細については、「 [Widening and Narrowing Conversions](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)」を参照してください。

変換プロシージャを `Widening` として宣言する場合、プロシージャ コードでエラーが発生しないようにする必要があります。 これは、次のことを意味します。

- 常に `type` 型の有効な値を返す必要があります。

- これは、可能性のあるすべての例外とその他のエラー条件を処理する必要があります。

- これが呼び出すすべてのプロシージャからのエラーを処理する必要があります。

変換プロシージャが成功しない可能性がある場合、または未処理の例外が発生する可能性がある場合は、それを `Narrowing` として宣言する必要があります。

## <a name="example"></a>例

次のコード例では、`Operator` ステートメントを使用して、`And`、`Or`、`IsFalse`、および `IsTrue` 演算子の演算子プロシージャを含む構造体のアウトラインを定義しています。 `And` および `Or` は、それぞれ `abc` 型の 2 つのオペランドを受け取り、`abc` 型を返します。 `IsFalse` および `IsTrue` は、それぞれ `abc` 型の 1 つのオペランドを受け取り、`Boolean` 型を返します。 これらの定義により、呼び出し元のコードでは、`abc` 型のオペランドを使用して、`And`、`AndAlso`、`Or`、および `OrElse` を使用できます。

[!code-vb[VbVbalrStatements#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#44)]

## <a name="see-also"></a>関連項目

- [IsFalse 演算子](../operators/isfalse-operator.md)
- [IsTrue 演算子](../operators/istrue-operator.md)
- [Widening](../modifiers/widening.md)
- [Narrowing](../modifiers/narrowing.md)
- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [演算子プロシージャ](../../programming-guide/language-features/procedures/operator-procedures.md)
- [方法: 演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [方法: 変換演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [方法: 演算子プロシージャを呼び出す](../../programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)
- [方法: 演算子を定義するクラスを使用する](../../programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)
