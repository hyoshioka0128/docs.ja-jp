---
title: データ型の有効な使用方法
ms.date: 07/20/2015
helpviewer_keywords:
- performance, data type efficiency
- data types [Visual Basic], weak typing
- AscW function [Visual Basic], preferred to Asc
- data types [Visual Basic], using efficiently
- optimization [Visual Basic], data types
- data types [Visual Basic], strong typing
- strong typing
- typing, strong
- data types [Visual Basic], optimizing
- ChrW function [Visual Basic], preferred to Chr
ms.assetid: 28f5e4ba-ec24-4f37-b90a-e8ee822f778a
ms.openlocfilehash: 0de02840cb18fde16134ef43df9d63abb503c979
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84394172"
---
# <a name="efficient-use-of-data-types-visual-basic"></a>データ型の有効な使用方法 (Visual Basic)
宣言されていない変数やデータ型なしで宣言された変数には、`Object` データ型が代入されます。 これにより、プログラムをすばやく簡単に記述できるようになりますが、実行速度が低下する可能性があります。

## <a name="strong-typing"></a>厳密な型指定
 すべての変数のデータ型を指定することを、"*厳密な型指定*" と呼びます。 厳密な型指定の使用には、いくつかの利点があります。

- これにより、変数の IntelliSense サポートが有効になります。 これにより、コードを入力しながら、プロパティとその他のメンバーを確認できます。

- コンパイラの型チェックを利用できます。 オーバーフローなどのエラーによって、実行時に失敗する可能性があるステートメントが取得されます。 また、メソッドをサポートしていないオブジェクトに対するそれらの呼び出しも取得されます。

- コードの実行時間が短縮されます。

## <a name="most-efficient-data-types"></a>最も効率的なデータ型
 小数が決して含まれない変数では、整数データ型が非整数型よりも効率的です。 Visual Basic では、`Integer` と `UInteger` が最も効率的な数値型です。

 小数について、`Double` が最も効率的なデータ型です。現在のプラットフォームのプロセッサが、倍精度で浮動小数点演算を実行するためです。 ただし、`Double` を使用した演算は、`Integer` などの整数型ほど高速ではありません。

## <a name="specifying-data-type"></a>データ型の指定
 [Dim ステートメント](../../../language-reference/statements/dim-statement.md)を使用して、特定の型の変数を宣言します。 次の例に示すように、[Public](../../../language-reference/modifiers/public.md)、[Protected](../../../language-reference/modifiers/protected.md)、[Friend](../../../language-reference/modifiers/friend.md)、または [Private](../../../language-reference/modifiers/private.md) キーワードを使用して、アクセス レベルを同時に指定できます。

```vb
Private x As Double
Protected s As String
```

## <a name="character-conversion"></a>文字の変換
 `AscW` 関数と `ChrW` 関数は Unicode で動作します。 これらを `Asc` や `Chr` (Unicode との間で変換を行う必要がある) よりも優先して使用する必要があります。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- [データの種類](index.md)
- [数値のデータ型](numeric-data-types.md)
- [変数宣言](../variables/variable-declaration.md)
- [IntelliSense の使用](/visualstudio/ide/using-intellisense)
