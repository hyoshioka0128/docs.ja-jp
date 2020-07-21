---
title: '方法: 新しい変数を作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- Dim statement [Visual Basic]
- variables [Visual Basic], creating
ms.assetid: 35300be3-77b0-4bef-a156-034d3cdedde0
ms.openlocfilehash: 501c8f3aff4c5b204d231bdc26213e13d125a7cf
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410530"
---
# <a name="how-to-create-a-new-variable-visual-basic"></a>方法: 新しい変数を作成する (Visual Basic)

[Dim ステートメント](../../../language-reference/statements/dim-statement.md)を使用して変数を作成します。

### <a name="to-create-a-new-variable"></a>新しい変数を作成するには

1. `Dim` ステートメントで変数を宣言します。

    ```vb
    Dim newCustomer
    ```

2. [Private](../../../language-reference/modifiers/private.md)、[Static](../../../language-reference/modifiers/static.md)、[Shadows](../../../language-reference/modifiers/shadows.md)、[WithEvents](../../../language-reference/modifiers/withevents.md) など、変数の特性の指定を含めます。 詳細については、「[宣言された要素の特性](../declared-elements/declared-element-characteristics.md)」を参照してください。

    ```vb
    Public Static newCustomer
    ```

    宣言で他のキーワードを使用する場合、`Dim` キーワードは必要ありません。

3. 指定の後ろに変数の名前を指定します。これは Visual Basic のルールおよび規則に従う必要があります。 詳細については、「[宣言された要素の名前](../declared-elements/declared-element-names.md)」を参照してください。

    ```vb
    Public Static newCustomer
    ```

4. 名前の後ろに [As](../../../language-reference/statements/as-clause.md) 句を指定して、変数のデータ型を指定します。

    ```vb
    Public Static newCustomer As Customer
    ```

    データ型を指定しない場合、既定値の `Object` が使用されます。

5. `As` 句の後ろに等号 (`=`) を指定し、等号の後ろに変数の初期値を指定します。

    Visual Basic により、`Dim` ステートメントが実行されるたびに、指定した値が変数に代入されます。 初期値を指定しない場合、Visual Basic では、`Dim` ステートメントを含むコードに初めて入ったときに、その変数のデータ型の既定の初期値が代入されます。

    変数が参照型である場合は、[New 演算子](../../../language-reference/operators/new-operator.md) キーワードを `As` 句に含めると、そのクラスのインスタンスを作成できます。 `New` を使用しない場合、変数の初期値は [Nothing](../../../language-reference/nothing.md) です。

    ```vb
    Public Static newCustomer As New Customer
    ```

## <a name="see-also"></a>関連項目

- [変数](index.md)
- [変数宣言](variable-declaration.md)
- [宣言された要素の名前](../declared-elements/declared-element-names.md)
- [宣言された要素の特性](../declared-elements/declared-element-characteristics.md)
- [Value Types and Reference Types](../data-types/value-types-and-reference-types.md)
- [ステートメント](../../../language-reference/statements/index.md)
- [ローカル型の推論](local-type-inference.md)
- [Option Infer ステートメント](../../../language-reference/statements/option-infer-statement.md)
