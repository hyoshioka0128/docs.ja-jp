---
title: => 演算子 - C# リファレンス
ms.custom: seodec18
ms.date: 01/22/2019
f1_keywords:
- =>_CSharpKeyword
helpviewer_keywords:
- lambda operator [C#]
- => operator [C#]
- lambda expressions [C#], => operator
ms.openlocfilehash: b8d1a4e3971eb30e76bf543497931ce029c5541d
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73036378"
---
# <a name="-operator-c-reference"></a>=> 演算子 (C# リファレンス)

`=>` トークンは、[ラムダ演算子](#lambda-operator)、および[式本体の定義](#expression-body-definition)におけるメンバー名とメンバー実装の区切り記号という 2 つの形式でサポートされています。

## <a name="lambda-operator"></a>ラムダ演算子

[ラムダ式](../../programming-guide/statements-expressions-operators/lambda-expressions.md)では、ラムダ演算子 `=>` により、左側の入力パラメーターと右側のラムダ本体とが分けられます。

次の例は、メソッド構文で [LINQ](../../programming-guide/concepts/linq/index.md) 機能を使用して、ラムダ式の使用法を示しています。

[!code-csharp-interactive[infer types of input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#InferredTypes)]

ラムダ式の入力パラメーターは、コンパイル時に厳密に型指定されます。 前の例のように、コンパイラが入力パラメーターの型を推論できる場合は、型宣言を省略できます。 入力パラメーターの型を指定する必要がある場合は、次の例に示すように、パラメーターごとに指定する必要があります。

[!code-csharp-interactive[specify types of input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#ExplicitTypes)]

次の例は、入力パラメーターを含まないラムダ式を定義する方法を示しています。

[!code-csharp-interactive[without input variables](~/samples/csharp/language-reference/operators/LambdaOperator.cs#WithoutInput)]

詳細については、「[ラムダ式](../../programming-guide/statements-expressions-operators/lambda-expressions.md)」を参照してください。

## <a name="expression-body-definition"></a>式本体の定義

式本体の定義には、次の一般的な構文があります。

```csharp
member => expression;
```

ここで、`expression` には有効な式を指定します。 `expression` の戻り値の型は、メンバーの戻り値の型に暗黙的に変換可能である必要があります。 メンバーの戻り値の型が `void` の場合や、メンバーがコンストラクター、ファイナライザー、またはプロパティ `set` のアクセサーの場合、`expression` は "[*ステートメント式*](~/_csharplang/spec/statements.md#expression-statements)" である必要があります。この場合は任意の型を指定できます。

次の例は、`Person.ToString` メソッドの式本体の定義を示しています。

```csharp
public override string ToString() => $"{fname} {lname}".Trim();
```

これは、次のメソッド定義の短縮形バージョンです。

```csharp
public override string ToString()
{
   return $"{fname} {lname}".Trim();
}
```

メソッド、演算子、および読み取り専用プロパティの式本体の定義は、C# 6 以降でサポートされています。 コンストラクター、ファイナライザー、プロパティ アクセサー、およびインデクサー アクセサーの式本体の定義は、C# 7.0 以降でサポートされています。

詳細については、「[式形式のメンバー](../../programming-guide/statements-expressions-operators/expression-bodied-members.md)」を参照してください。

## <a name="operator-overloadability"></a>演算子のオーバーロード可/不可

`=>` 演算子はオーバーロードできません。

## <a name="c-language-specification"></a>C# 言語仕様

ラムダ演算子の詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の[匿名関数の式](~/_csharplang/spec/expressions.md#anonymous-function-expressions)に関するセクションを参照してください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# 演算子](index.md)
