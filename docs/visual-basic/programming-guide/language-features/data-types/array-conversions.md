---
title: 配列の変換
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [Visual Basic], converting type
- type conversion [Visual Basic], arrays
- conversions [Visual Basic], type
- arrays [Visual Basic], data types
- conversions [Visual Basic], data type
- object arrays [Visual Basic], converting type
- data type conversion [Visual Basic], array conversions
- conversions [Visual Basic], array types
- object arrays
ms.assetid: fceff7d2-a1b7-44c7-b9aa-8bd831d8a444
ms.openlocfilehash: 1d20b01200d3f967e3355dc6e9651291003d140e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402006"
---
# <a name="array-conversions-visual-basic"></a>配列の変換 (Visual Basic)
次の条件を満たす場合は、配列型を別の配列型に変換できます。  
  
- **ランクが同じ。** 2 つの配列のランクは同じであることが必要です。つまり、含まれる次元の数が同じである必要があります。 ただし、それぞれの次元の長さは同じでなくてもかまいません。  
  
- **要素のデータ型。** 両方の配列の要素のデータ型は、参照型である必要があります。 `Integer` 配列を `Long` 配列、あるいは `Object` 配列に変換することはできません。これは、少なくとも 1 つの値型が関係するためです。 詳細については、「 [Value Types and Reference Types](value-types-and-reference-types.md)」を参照してください。  
  
- **互換性。** 2 つの配列の要素型の間で、変換 (拡大または縮小) を実行できる必要があります。 たとえば、`String` 配列と <xref:System.Attribute?displayProperty=nameWithType> から派生したクラスの配列との間での変換を試行した場合は、この要件が満たされません。 これらの 2 つの型には共通点がなく、これらの間ではどのような種類の変換も行われません。  
  
 ある配列型から別の配列型への変換が、拡大と縮小のどちらであるかは、それぞれの要素の変換が拡大であるか縮小であるかに応じて決まります。 詳細については、「 [Widening and Narrowing Conversions](widening-and-narrowing-conversions.md)」を参照してください。  
  
## <a name="conversion-to-an-object-array"></a>オブジェクト配列への変換  
 初期化せずに `Object` 配列を宣言すると、初期化されない限り、その要素の型は `Object` です。 これを特定のクラスの配列に設定すると、そのクラスの型を引き継ぎます。 ただし、基になる型はまだ `Object` であり、その後、関連しないクラスの別の配列に設定できます。 すべてのクラスは `Object` から派生するため、配列の要素型はどのクラスでも別のクラスに変更できます。  
  
 次の例では `student` と `String` 型の間に変換は存在しませんが、両方とも `Object` から派生しているので、すべての代入が有効です。  
  
```vb  
' Assume student has already been defined as a class.  
Dim testArray() As Object  
' testArray is still an Object array at this point.  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
testArray = New student(3) {}  
' testArray is now of type student().  
testArray = names  
' testArray is now a String array.  
```  
  
### <a name="underlying-type-of-an-array"></a>配列の基になる型  
 最初に特定のクラスを使用して配列を宣言した場合、基になる要素型はそのクラスになります。 後でそれを別のクラスの配列に設定する場合は、2 つのクラス間の変換が必要です。  
  
 次の例では、`students` は `student` 配列です。 `String` と `student` の間に変換が存在しないため、最後のステートメントは失敗します。  
  
```vb  
Dim students() As student  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
students = New Student(3) {}  
' The following statement fails at compile time.  
students = names  
```  
  
## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [Visual Basic における型変換](type-conversions.md)
- [暗黙の型変換と明示的な型変換](implicit-and-explicit-conversions.md)
- [文字列とその他の型との変換](conversions-between-strings-and-other-types.md)
- [方法: Visual Basic でオブジェクトを別の型に変換する](how-to-convert-an-object-to-another-type.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)
- [配列](../arrays/index.md)
