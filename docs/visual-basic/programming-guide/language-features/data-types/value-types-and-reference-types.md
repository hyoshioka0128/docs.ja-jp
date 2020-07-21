---
title: 値型と参照型
ms.date: 07/20/2015
helpviewer_keywords:
- reference data types [Visual Basic]
- reference types [Visual Basic]
- value types [Visual Basic]
- value data types [Visual Basic]
- types [Visual Basic]
- data types [Visual Basic], value types
- data types [Visual Basic], reference types
ms.assetid: fc82ce15-5a40-4c5c-a1e1-a556830e7391
ms.openlocfilehash: 3a1de120f5f97ba93939f332f121d70cd3091216
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392975"
---
# <a name="value-types-and-reference-types"></a>値型と参照型
Visual Basic には、参照型と値型という 2 種類の型があります。 参照型の変数はデータ (オブジェクト) への参照を格納するのに対して、値型の変数はデータを直接格納します。 参照型の場合、2 つの変数が同じオブジェクトを参照できるため、ある変数に対する演算によって、他の変数が参照しているオブジェクトが影響を受ける可能性があります。 値型の場合、各変数が独自のデータ コピーを保持し、ある変数に対する操作が別の変数に影響を与えることはありません ([パラメーターの ByRef 修飾子](../../../language-reference/modifiers/byref.md)の場合を除きます)。
  
## <a name="value-types"></a>値型  
 データ型は、独自のメモリ割り当てでデータを保持する場合、"*値型*" です。 値型は、次のとおりです。  
  
- すべての数値データ型  
  
- `Boolean`、 `Char`、および `Date`  
  
- すべての構造体 (メンバーが参照型の場合であっても)  
  
- 列挙体 (基になる型が常に `SByte`、`Short`、`Integer`、`Long`、`Byte`、`UShort`、`UInteger`、または `ULong` であるため)  
  
 すべての構造体は、参照型のメンバーが含まれている場合でも、値型です。 このため、`Char` や `Integer` などの値型は .NET Framework 構造体によって実装されます。  
  
 予約済みのキーワード (`Decimal`など) を使用して値型を宣言できます。 `New` キーワードを使用して値型を初期化することもできます。 これは、型にパラメーターを受け取るコンストラクターがある場合に特に便利です。 この例として、指定したパーツから新しい `Decimal` 値を構築する <xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29> コンストラクターがあります。  
  
## <a name="reference-types"></a>参照型  
 "*参照型*" はデータへの参照を格納します。 参照型は、次のとおりです。  
  
- `String`  
  
- すべての配列 (要素が値型であっても)  
  
- <xref:System.Windows.Forms.Form> などのクラス型  
  
- デリゲート  
  
 クラスは "*参照型*" です。 すべての配列は参照型であることにご注意ください。これは、そのメンバーが値型の場合でも同様です。  
  
 参照型はすべて、基になる .NET Framework クラスを表しているため、初期化するときは [New 演算子](../../../language-reference/operators/new-operator.md)キーワードを使用する必要があります。 次のステートメントで配列を初期化します。  
  
```vb  
Dim totals() As Single = New Single(8) {}  
```  
  
## <a name="elements-that-are-not-types"></a>型ではない要素  
 次のプログラミング要素は、宣言した要素のデータ型として指定できないため、型としては使用できません。  
  
- 名前空間  
  
- モジュール  
  
- イベント  
  
- プロパティとプロシージャ  
  
- 変数、定数、フィールド  
  
## <a name="working-with-the-object-data-type"></a>オブジェクト データ型の使用  
 `Object` データ型の変数には、参照型または値型のどちらでも割り当てることができます。 `Object` 変数では、データ自体ではなく、常にデータへの参照が保持されます。 ただし、`Object` 変数に値型を割り当てた場合は、独自のデータを保持しているかのような動作になります。 詳細については、「[Object データ型](../../../language-reference/data-types/object-data-type.md)」を参照してください。  
  
 `Object` 変数が参照型と値型のどちらとして機能しているかを確認するには、<xref:Microsoft.VisualBasic?displayProperty=nameWithType> 名前空間の <xref:Microsoft.VisualBasic.Information> クラスの <xref:Microsoft.VisualBasic.Information.IsReference%2A> メソッドにそれを渡します。 `Object` 変数の内容が参照型を表している場合、<xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=nameWithType> で `True` が返されます。  
  
## <a name="see-also"></a>関連項目

- [null 許容値型](nullable-value-types.md)
- [Visual Basic における型変換](type-conversions.md)
- [Structure ステートメント](../../../language-reference/statements/structure-statement.md)
- [データ型の有効な使用方法](efficient-use-of-data-types.md)
- [Object 型](../../../language-reference/data-types/object-data-type.md)
- [データの種類](index.md)
