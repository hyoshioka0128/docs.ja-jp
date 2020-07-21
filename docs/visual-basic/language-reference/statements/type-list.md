---
title: 型リスト
ms.date: 07/20/2015
f1_keywords:
- StructureConstraint
- vb.StructureConstraint
- ClassConstraint
- vb.ClassConstraint
helpviewer_keywords:
- class constraint
- constraints, Visual Basic generic types
- generic parameters
- generics [Visual Basic], constraints
- generics [Visual Basic], type list
- structure constraint
- constraints, in type parameters
- generics [Visual Basic], generic types
- parameters [Visual Basic], type
- constraints, Structure keyword
- type parameters [Visual Basic], constraints
- types [Visual Basic], generic
- parameters [Visual Basic], generic
- generics [Visual Basic], type parameters
- type parameters
- constraints, Class keyword
ms.assetid: 56db947a-2ae8-40f2-a70a-960764e9d0db
ms.openlocfilehash: 7e22ad6e32ec13f081391e1d47a80df8b1e65063
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84412989"
---
# <a name="type-list-visual-basic"></a>型リスト (Visual Basic)

*ジェネリック* プログラミング要素の*型パラメーター*を指定します。 複数のパラメーターはコンマで区切ります。 次に、1 つの型パラメーターの構文を示します。

## <a name="syntax"></a>構文

```vb
[genericmodifier] typename [ As constraintlist ]
```

## <a name="parts"></a>指定項目

|用語|定義|
|---|---|
|`genericmodifier`|任意。 ジェネリック インターフェイスとデリゲートのみで使用できます。 [Out](../modifiers/out-generic-modifier.md) キーワードを使用して共変として、または [In](../modifiers/in-generic-modifier.md) キーワードを使用して反変として、型を宣言できます。 「 [共変性と反変性](../../programming-guide/concepts/covariance-contravariance/index.md)を参照してください。|
|`typename`|必須です。 型パラメーターの名前。 これは、対応する型引数で提供された、定義済みの型に置換されるプレースホルダーです。|
|`constraintlist`|任意。 `typename` に指定できるデータ型を制約する要件の一覧。 複数の制約がある場合は、それらを中かっこ (`{ }`) で囲み、コンマで区切ります。 [As](as-clause.md) キーワードを使用して、制約リストを取り込む必要があります。 `As` は、リストの開始で 1 回だけ使用します。|

## <a name="remarks"></a>Remarks

すべてのジェネリック プログラミング要素で、少なくとも 1 つの型パラメーターを受け取る必要があります。 型パラメーターは、クライアント コードでジェネリック型のインスタンスを作成するときに指定する特定の型 (*構築された要素*) のプレースホルダーです。 ジェネリック クラス、構造体、インターフェイス、プロシージャ、またはデリゲートを定義できます。

ジェネリック型を定義する場合の詳細については、「[Visual Basic におけるジェネリック型](../../programming-guide/language-features/data-types/generic-types.md)」を参照してください。 型パラメーター名の詳細については、「[宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。

## <a name="rules"></a>ルール

- **かっこ。** 型パラメーター リストを指定する場合は、かっこで囲む必要があります。また、[Of](of-clause.md) キーワードでリストを取り込む必要があります。 `Of` は、リストの開始で 1 回だけ使用します。

- **制約。** 型パラメーターへの*制約*の一覧には、次の項目を任意の組み合わせで含めることができます。

  - 任意の数のインターフェイス。 指定された型では、この一覧のすべてのインターフェイスを実装する必要があります。

  - 最大 1 つのクラス。 指定した型は、そのクラスから継承する必要があります。

  - `New` キーワード。 指定した型では、ジェネリック型でアクセスできるパラメーターなしのコンストラクターを公開する必要があります。 これは、1 つまたは複数のインターフェイスによって型パラメーターを制約する場合に便利です。 インターフェイスを実装する型では、必ずしもコンストラクターが公開されているとは限らず、コンストラクターのアクセス レベルによっては、ジェネリック型内のコードでそれにアクセスできない場合があります。

  - `Class` キーワードまたは `Structure` キーワード。 `Class` キーワードでは、ジェネリック型パラメーターを制約して、すべての型引数が参照型 (文字列、配列、デリゲート、またはクラスから作成されたオブジェクトなど) として渡されることを必要とします。 `Structure` キーワードでは、ジェネリック型パラメーターを制約して、すべての型引数が値型 (構造体、列挙型、基本データ型など) として渡されることを必要とします。 `Class` と `Structure` を同じ `constraintlist` に含めることはできません。

  指定した型は、`constraintlist` に含まれるすべての要件を満たしている必要があります。

  各型パラメーターに対する制約は、他の型パラメーターに対する制約と関係がありません。

## <a name="behavior"></a>動作

- **コンパイル時置換。** ジェネリック プログラミング要素から構築された型を作成する場合は、各型パラメーターに定義済みの型を指定します。 Visual Basic コンパイラによって、ジェネリック要素内の `typename` のすべての存在について、指定した型が使われます。

- **制約なし。** 型パラメーターに対して制約を指定しない場合、コードは、その型パラメーターの[オブジェクト データ型](../data-types/object-data-type.md)でサポートされる操作とメンバーに制限されます。

## <a name="example"></a>例

次の例に、ジェネリック ディクショナリ クラスのスケルトン定義を示しています。これには、新しいエントリをディクショナリに追加するスケルトン関数も含まれます。

[!code-vb[VbVbalrStatements#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#3)]

## <a name="example"></a>例

`dictionary` はジェネリックであるため、それを使用するコードでは、それぞれが同じ機能を持ちながらも、異なるデータ型に対して動作する、さまざまなオブジェクトを作成できます。 次の例に、`String` エントリと `Integer` キーを含む `dictionary` オブジェクトを作成するコード行を示しています。

[!code-vb[VbVbalrStatements#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#4)]

## <a name="example"></a>例

次の例は、前の例で生成された同等のスケルトン定義を示しています。

[!code-vb[VbVbalrStatements#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#5)]

## <a name="see-also"></a>関連項目

- [Of](of-clause.md)
- [New 演算子](../operators/new-operator.md)
- [Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)
- [Object 型](../data-types/object-data-type.md)
- [Function ステートメント](function-statement.md)
- [Structure ステートメント](structure-statement.md)
- [Sub ステートメント](sub-statement.md)
- [方法: ジェネリック クラスを使用する](../../programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [共変性と反変性](../../programming-guide/concepts/covariance-contravariance/index.md)
- [In](../modifiers/in-generic-modifier.md)
- [Out](../modifiers/out-generic-modifier.md)
