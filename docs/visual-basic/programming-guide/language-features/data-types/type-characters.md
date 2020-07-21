---
title: 型文字
ms.date: 01/31/2018
helpviewer_keywords:
- '&H prefix for hexadecimal values'
- hexadecimal literals [Visual Basic]
- F literal type character [Visual Basic]
- '& identifier type character'
- type characters [Visual Basic]
- octal literals [Visual Basic]
- literals [Visual Basic], hexadecimal
- '&O prefix for octal values'
- literals [Visual Basic], default types
- defaults, literal types
- C literal type character [Visual Basic]
- type characters [Visual Basic], literal
- $ identifier type character
- L literal type character [Visual Basic]
- UI literal type characters [Visual Basic]
- default literal types [Visual Basic]
- D literal type character [Visual Basic]
- literals [Visual Basic], octal
- S literal type character [Visual Basic]
- '! identifier type character'
- US literal type characters [Visual Basic]
- '% identifier type character'
- data types [Visual Basic], type characters
- characters [Visual Basic], identifier type
- type characters [Visual Basic], identifier
- '# identifier type character'
- identifier type characters [Visual Basic]
- literal type characters [Visual Basic]
- I literal type character [Visual Basic]
- R literal type character [Visual Basic]
- '@ identifier type character'
- UL literal type characters [Visual Basic]
- literal types [Visual Basic], default
ms.assetid: 6353cb9b-6ee4-4af6-a5a8-88ce39f90cc5
ms.openlocfilehash: a48260694c1dfcbbb8f804f220fe89b1663c7319
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393079"
---
# <a name="type-characters-visual-basic"></a>型文字 (Visual Basic)

宣言ステートメントでデータ型を指定するだけでなく、"*型文字*" を使用して一部のプログラミング要素のデータ型を強制的に指定することもできます。 型文字は、要素の直後に指定する必要があります。その間にはどのような種類の文字も指定できません。

型文字は、要素の名前の一部ではありません。 型文字で定義された要素は、型文字を使用せずに参照できます。

## <a name="identifier-type-characters"></a>識別子の型文字

Visual Basic には、変数または定数のデータ型を指定するために宣言で使用できる、一連の "*識別子の型文字*" が用意されています。 使用できる識別子の型文字と使用例を次の表に示します。
  
|識別子の型文字|データの種類|例|  
|-------------------------------|---------------|-------------|  
|`%`|`Integer`|`Dim L%`|  
|`&`|`Long`|`Dim M&`|  
|`@`|`Decimal`|`Const W@ = 37.5`|  
|`!`|`Single`|`Dim Q!`|  
|`#`|`Double`|`Dim X#`|  
|`$`|`String`|`Dim V$ = "Secret"`|  
  
 `Boolean`、`Byte`、`Char`、`Date`、`Object`、`SByte`、`Short`、`UInteger`、`ULong`、または `UShort` データ型、あるいは配列や構造体などの複合データ型には、識別子の型文字はありません。

場合によっては、`$` 文字を Visual Basic 関数に追加して (`Left` ではなく `Left$` など)、`String` 型の戻り値を取得することもできます。

すべての場合で、識別子の型文字は識別子名の直後に指定する必要があります。

## <a name="literal-type-characters"></a>リテラルの型文字

"*リテラル*" は、あるデータ型の特定の値のテキスト表現です。  

### <a name="default-literal-types"></a>既定のリテラル型

通常は、コードに表示されるリテラルの形式によって、そのデータ型が決まります。 次の表に既定の型を示します。  
  
|テキスト形式のリテラル|既定のデータ型|例|  
|-----------------------------|-----------------------|-------------|  
|数値、小数部なし|`Integer`|`2147483647`|  
|数値、小数部なし、`Integer` には大きすぎる|`Long`|`2147483648`|  
|数値、小数部あり|`Double`|`1.2`|  
|二重引用符で囲まれている|`String`|`"A"`|  
|シャープ記号で囲まれている|`Date`|`#5/17/1993 9:32 AM#`|  

### <a name="forced-literal-types"></a>強制リテラル型

Visual Basic には一連の "*リテラルの型文字*" が用意されています。これらを使用して、リテラルの形式が示すデータ型以外のデータ型に強制的に変更できます。 これを行うには、リテラルの末尾に文字を追加します。 使用できるリテラルの型文字と使用例を次の表に示します。
  
|リテラルの型文字|データの種類|例|  
|----------------------------|---------------|-------------|  
|`S`|`Short`|`I = 347S`|
|`I`|`Integer`|`J = 347I`|
|`L`|`Long`|`K = 347L`|
|`D`|`Decimal`|`X = 347D`|
|`F`|`Single`|`Y = 347F`|
|`R`|`Double`|`Z = 347R`|
|`US`|`UShort`|`L = 347US`|
|`UI`|`UInteger`|`M = 347UI`|
|`UL`|`ULong`|`N = 347UL`|
|`C`|`Char`|`Q = "."C`|

`Boolean`、`Byte`、`Date`、`Object`、`SByte`、または `String` データ型、あるいは配列や構造体などの複合データ型には、リテラルの型文字はありません。

リテラルは、変数、定数、および式と同様に、識別子の型文字(`%`、`&`、`@`、`!`、`#`、`$`) も使用できます。 ただし、リテラルの型文字 (`S`、`I`、`L`、`D`、`F`、`R`、`C`) はリテラルでしか使用できません。

すべての場合で、リテラルの型文字はリテラル値の直後に指定する必要があります。

## <a name="hexadecimal-binary-and-octal-literals"></a>16 進数、2 進数、および 8 進数のリテラル

通常、コンパイラは、整数リテラルを 10 進法 (基数 10) で解釈します。 整数リテラルは、`&H` プレフィックスを使用して 16 進法 (基数 16) として、`&B` プレフィックスを使用して 2 進法 (基数 2) として、また `&O` プレフィックスを使用して 8 進法 (基数 8) として定義することもできます。 プレフィックスの後の数字は、その記数法に適している必要があります。 次の表に例を示します。  
  
|基数|プレフィックス|有効な数値|例|
|-----------------|------------|------------------------|-------------|
|16 進数 (基数 16)。|`&H`|0 - 9 および A - F|`&HFFFF`|
|2 進数 (基数 2)|`&B`|0-1|`&B01111100`|
|8 進数 (基数 8)。|`&O`|0-7|`&O77`|

Visual Basic 2017 以降では、アンダースコア文字 (`_`) をグループ区切り記号として使用して、整数リテラルを読みやすくすることができます。 次の例では、`_` 文字を使用して、2 進数リテラルを 8 ビットずつのグループにグループ化しています。

```vb
Dim number As Integer = &B00100010_11000101_11001111_11001101
```

プレフィックス付きリテラルの後にリテラルの型文字を指定できます。 次に例を示します。

```vb
Dim counter As Short = &H8000S
Dim flags As UShort = &H8000US
```

前の例では、`counter` は 10 進値 -32768、`flags` は 10 進値 +32768 を含みます。

Visual Basic 15.5 以降では、プレフィックスと 16 進数、2 進数、または 8 進数の間に先頭の区切り記号としてアンダースコア文字 (`_`) を使用することもできます。 次に例を示します。

```vb
Dim number As Integer = &H_C305_F860
```

[!INCLUDE [supporting-underscores](../../../../../includes/vb-separator-langversion.md)]

## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [基本データ型](elementary-data-types.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [Visual Basic における型変換](type-conversions.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
- [変数宣言](../variables/variable-declaration.md)
- [データの種類](../../../language-reference/data-types/index.md)
