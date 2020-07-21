---
title: 複合データ型
ms.date: 04/25/2017
helpviewer_keywords:
- classes [Visual Basic], composite data types
- composite types [Visual Basic]
- composite data types [Visual Basic]
- data types [Visual Basic], composite
- arrays [Visual Basic], composite data types
- structures [Visual Basic], composite data types
- classes [Visual Basic], composite types
- types [Visual Basic], composite
ms.assetid: 62970f2e-52c0-4369-8963-613820f1f434
ms.openlocfilehash: 3e8df5ccfeca4bc0a19237ba6d59e9d0747080ea
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84394299"
---
# <a name="composite-data-types-visual-basic"></a>複合データ型 (Visual Basic)
Visual Basic で用意されている基本データ型に加え、さまざまな型の項目を組み合わせて、構造体、配列、クラスなどの "*複合データ型*" を作成することもできます。 複合データ型は、基本型および他の複合型から構築できます。 たとえば、構造体要素の配列、または配列メンバーを含む構造体を定義できます。  
  
## <a name="data-types"></a>データの種類  
 複合型は、その構成要素いずれかのデータ型とは異なります。 たとえば、`Integer` 要素の配列は `Integer` データ型ではありません。  
  
 通常、配列のデータ型は、必要に応じて、要素の型、かっこ、およびコンマを使用して表されます。 たとえば、`String` 要素の 1 次元配列は `String()` と表され、`Boolean` 要素の 2 次元配列は `Boolean(,)` と表されます。  
  
## <a name="structure-types"></a>構造体型  
 すべての構造体に対応する 1 つのデータ型はありません。 2 つの構造体で同じ要素が同じ順序で定義されている場合でも、構造体のそれぞれの定義は一意のデータ型を表します。 ただし、同じ構造体の複数のインスタンスを作成した場合、Visual Basic では、それらが同じデータ型と見なされます。  
  
## <a name="tuples"></a>タプル

タプルは、型が事前定義された複数のフィールドを含む軽量の構造体です。 タプルは Visual Basic 2017 以降でサポートされています。 タプルは、1 回のメソッド呼び出しで複数の値を返す際に最もよく使用されます。参照によって引数を渡したり、返されたフィールドをより重いクラスまたは構造体にパッケージ化したりする必要はありません。 タプルの詳細については、「[タプル](tuples.md)」のトピックを参照してください。

## <a name="array-types"></a>配列型  
 すべての配列に対応する 1 つのデータ型はありません。 配列の特定のインスタンスのデータ型は、次によって決まります。  
  
- 配列であるという事実  
  
- 配列のランク (次元数)  
  
- 配列の要素型  
  
 特に、所定のディメンションの長さは、インスタンスのデータ型には含まれません。 次の例を使って説明します。  
  
```vb  
Dim arrayA( ) As Byte = New Byte(12) {}  
Dim arrayB( ) As Byte = New Byte(100) {}  
Dim arrayC( ) As Short = New Short(100) {}  
Dim arrayD( , ) As Short  
Dim arrayE( , ) As Short = New Short(4, 10) {}  
```  
  
 前の例で、配列変数 `arrayA` および `arrayB` は、別の長さに初期化されていますが、同じデータ型 (`Byte()`) と見なされます。 変数 `arrayB` および `arrayC` は、要素の型が異なるため、同じ型ではありません。 変数 `arrayC` および `arrayD` は、ランクが異なるため、同じ型ではありません。 変数 `arrayD` および `arrayE` は、ランクと要素の型が同じであるため同じ型 (`Short(,)`) です。ただし、`arrayD` はまだ初期化されていません。  
  
 配列の詳細については、「[配列](../arrays/index.md)」を参照してください。  
  
## <a name="class-types"></a>クラスの種類  
 すべてのクラスに対応する 1 つのデータ型はありません。 1 つのクラスは別のクラスを継承できますが、それぞれは個別のデータ型です。 同じクラスの複数のインスタンスは同じデータ型です。 あるクラス インスタンス変数を別のクラス インスタンス変数に代入すると、データ型が同じになるだけでなく、メモリ内の同じクラス インスタンスを参照します。  
  
 クラスの詳細については、[オブジェクトとクラス](../objects-and-classes/index.md)に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [基本データ型](elementary-data-types.md)
- [Generic Types in Visual Basic](generic-types.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [Visual Basic における型変換](type-conversions.md)
- [構造体](structures.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
- [方法: 変数内で複数の値を保持する](how-to-hold-more-than-one-value-in-a-variable.md)
