---
title: '方法: 変数内で複数の値を保持する'
ms.date: 07/20/2015
helpviewer_keywords:
- classes [Visual Basic], composite data types
- composite types [Visual Basic]
- composite data types [Visual Basic]
- data types [Visual Basic], composite
- arrays [Visual Basic], composite data types
- structures [Visual Basic], composite data types
- arrays [Visual Basic], compilation errors
- types [Visual Basic], composite
ms.assetid: 5fe0e558-aac2-4a40-b7f2-7cfea7336917
ms.openlocfilehash: 399c5909ee6988f96bcc85260b0401f3bd18a0f2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393897"
---
# <a name="how-to-hold-more-than-one-value-in-a-variable-visual-basic"></a>方法: 変数内で複数の値を保持する (Visual Basic)

変数に複数の値が保持されるのは、"*複合データ型*" として宣言したときです。

[複合データ型](composite-data-types.md)には、構造体、配列、およびクラスが含まれます。 複合データ型の変数は、基本データ型とその他の複合型の組み合わせを保持できます。 構造体とクラスは、データだけでなくコードも保持できます。

## <a name="to-hold-more-than-one-value-in-a-variable"></a>変数内で複数の値を保持するには

1. 変数でどの複合データ型を使用するかを決定します。

2. その複合データ型がまだ定義されていない場合、定義すると変数で使用できるようになります。

    - [Structure ステートメント](../../../language-reference/statements/structure-statement.md)を使用して構造体を定義します。

    - [Dim ステートメント](../../../language-reference/statements/dim-statement.md)を使用して配列を定義します。

    - [Class ステートメント](../../../language-reference/statements/class-statement.md)を使用してクラスを定義します。

3. `Dim` ステートメントを使用して変数を宣言します。

4. 変数名の後に `As` 句を指定します。

5. `As` キーワードに続けて、適切な複合データ型の名前を指定します。

## <a name="see-also"></a>関連項目

- [データの種類](../../../language-reference/data-types/index.md)
- [型文字](type-characters.md)
- [複合データ型](composite-data-types.md)
- [構造体](structures.md)
- [配列](../arrays/index.md)
- [クラスとオブジェクト](../objects-and-classes/index.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
