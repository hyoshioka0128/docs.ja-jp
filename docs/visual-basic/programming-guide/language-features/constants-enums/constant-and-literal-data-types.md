---
title: 定数とリテラルのデータ型
ms.date: 07/20/2015
helpviewer_keywords:
- declaring constants [Visual Basic], literal data types
- data types [Visual Basic], declaring
- constants [Visual Basic], declaring
- explicit declarations
- literals [Visual Basic], coercing data type
- declarations [Visual Basic], data types
ms.assetid: 057206d2-3a5b-40b9-b3af-57446f9b52fa
ms.openlocfilehash: b94259326b42104db05d9fc5bb09f686075d0759
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414532"
---
# <a name="constant-and-literal-data-types-visual-basic"></a>定数とリテラルのデータ型 (Visual Basic)
リテラルとは、数字の 3 や文字列 "Hello" など、変数値や式の結果ではなく、それ自体として表される値のことです。 定数とは、リテラルの代わりとなるわかりやすい名前のことです。プログラム内で値が変わりうる変数とは異なり、プログラム全体で同じ値を保持します。  
  
 [Option Infer](../../../language-reference/statements/option-infer-statement.md) に `Off` を指定し、[Option Strict](../../../language-reference/statements/option-strict-statement.md) に `On` を指定した場合、すべての定数にデータ型を指定して明示的に宣言する必要があります。 次の例では、`MyByte` のデータ型をデータ型 `Byte` として明示的に宣言しています。  
  
 [!code-vb[VbVbalrConstants#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#1)]  
  
 `Option Infer` に `On` を指定するか、`Option Strict` に `Off` を指定している場合は、`As` 句でデータ型を指定することなく定数を宣言できます。 コンパイラは、式の型から定数の型を判断します。 既定では、数値整数型のリテラルは `Integer` データ型にキャストされます。 浮動小数点数の既定のデータ型は `Double` であり、 `Boolean` 定数は `True` と `False` の各キーワードで指定します。  
  
## <a name="literals-and-type-coercion"></a>リテラルと強制型変換  
 `Decimal` 型変数に非常に大きな整数型リテラルの値を割り当てる場合など、リテラルの特定のデータ型への強制変換が必要になることがあります。 次の例ではエラーが発生します。  
  
```vb  
Dim myDecimal as Decimal  
myDecimal = 100000000000000000000   ' This causes a compiler error.  
```  
  
 このエラーの原因は、リテラルの表現にあります。 `Decimal` データ型はこの大きさの値を保持できますが、リテラルは暗黙的に `Long` として表現されるので、値を保持できません。  
  
 リテラルは、2 つの方法で特定のデータ型に強制的に変換できます。1 つは型文字をリテラルに追加することであり、もう 1 つは囲み文字内にリテラルを配置することです。 型文字と囲み文字は、リテラルの直前または直後に、スペースや文字を挟まずに配置する必要があります。  
  
 前述の例を機能させるには、リテラルに `D` 型文字を追加します。これにより、リテラルが `Decimal` として表現されます。  
  
 [!code-vb[VbVbalrConstants#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#2)]  
  
 型文字と囲み文字の正しい使用方法を、次の例に示します。  
  
 [!code-vb[VbVbalrConstants#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#3)]  
  
 Visual Basic で利用可能な囲み文字と囲み文字を、次の表に示します。  
  
|データの種類|囲み文字|追加する型文字|  
|---|---|---|  
|`Boolean`|(なし)|(なし)|  
|`Byte`|(なし)|(なし)|  
|`Char`|"|C|  
|`Date`|#|(なし)|  
|`Decimal`|(なし)|D または @|  
|`Double`|(なし)|R または #|  
|`Integer`|(なし)|I または %|  
|`Long`|(なし)|L または &|  
|`Short`|(なし)|S|  
|`Single`|(なし)|F または !|  
|`String`|"|(なし)|  
  
## <a name="see-also"></a>関連項目

- [ユーザー定義定数](user-defined-constants.md)
- [方法: 定数を宣言する](how-to-declare-a-constant.md)
- [定数の概要](constants-overview.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
- [Option Explicit ステートメント](../../../language-reference/statements/option-explicit-statement.md)
- [列挙型の概要](enumerations-overview.md)
- [方法: 列挙型を宣言する](how-to-declare-enumerations.md)
- [列挙型と名前の修飾](enumerations-and-name-qualification.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [定数と列挙体](../../../language-reference/constants-and-enumerations.md)
