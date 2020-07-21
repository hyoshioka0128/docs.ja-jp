---
title: '方法: 値の変わらない変数を作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], read-only
- variables [Visual Basic], constant value
ms.assetid: 86b59266-25df-4635-ae15-9b59c411d036
ms.openlocfilehash: 04e08784b5cfbdeb6db73b9b00fe9afa201bd06d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410517"
---
# <a name="how-to-create-a-variable-that-does-not-change-in-value-visual-basic"></a>方法: 値の変わらない変数を作成する (Visual Basic)

値の変わらない変数の概念は、矛盾しているように見えるかもしれません。 しかし、定数を使用することができず、固定値を持つ変数を用意すると便利な場合があります。 そのような場合は、[ReadOnly](../../../language-reference/modifiers/readonly.md) キーワードを使用してメンバー変数を定義することができます。

次のような状況では、[Const ステートメント](../../../language-reference/statements/const-statement.md)を使用して定数値の宣言および割り当てを行うことはできません。

- 使用したいデータ型を `Const` ステートメントに指定できない

- コンパイル時に値がわからない

- コンパイル時に定数値を計算できない

### <a name="to-create-a-variable-that-does-not-change-in-value"></a>値の変わらない変数を作成するには

1. モジュール レベルで、[Dim ステートメント](../../../language-reference/statements/dim-statement.md)を使用してメンバー変数を宣言し、[ReadOnly](../../../language-reference/modifiers/readonly.md) キーワードを含めます。

    ```vb
    Dim ReadOnly timeStarted
    ```

    `ReadOnly` は、メンバー変数に対してのみ指定できます。 つまり、プロシージャの外部で、モジュール レベルで、この変数を定義する必要があります。

2. コンパイル時に単一のステートメントで値を計算できる場合は、`Dim` ステートメントで初期化句を使用します。 [As](../../../language-reference/statements/as-clause.md) 句の後に等号 (`=`) を置き、その後に式を続けます。 コンパイラがこの式を定数値に評価できることを確認してください。

    ```vb
    Dim ReadOnly timeStarted As Date = Now
    ```

    `ReadOnly` 変数に値を割り当てることができるのは 1 回だけです。 一度それを行うと、コードによってその値を変更することはできません。

    コンパイル時に値がわからない場合、またはコンパイル時に単一のステートメントで値を計算できない場合でも、実行時にコンストラクター内でそれを割り当てることができます。 これを行うには、クラスまたは構造体のレベルで `ReadOnly` 変数を宣言する必要があります。 そのクラスまたは構造体のコンストラクターで、変数の固定値を計算し、それを変数に割り当てたら、コンストラクターから戻ります。

## <a name="see-also"></a>関連項目

- [WriteOnly](../../../language-reference/modifiers/writeonly.md)
- [Const ステートメント](../../../language-reference/statements/const-statement.md)
