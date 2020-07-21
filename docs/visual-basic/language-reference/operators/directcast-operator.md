---
title: DirectCast 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.directCast
- directCast
helpviewer_keywords:
- DirectCast keyword [Visual Basic]
ms.assetid: 63e5a1d0-4d9e-4732-bf8f-e90c0c8784b8
ms.openlocfilehash: 96cb2082d59373deb34d6894270205b7c1045850
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371519"
---
# <a name="directcast-operator-visual-basic"></a>DirectCast 演算子 (Visual Basic)
継承または実装に基づく型変換操作を導入します。  
  
## <a name="remarks"></a>Remarks  
 `DirectCast` では、変換に Visual Basic ランタイム ヘルパー ルーチンが使用されないため、データ型 `Object` 間で変換を行う場合、`CType` よりも多少パフォーマンスが向上する可能性があります。  
  
 `DirectCast` キーワードは、[CType 関数](../functions/ctype-function.md)および [TryCast 演算子](trycast-operator.md)キーワードを使用するのと同じ方法で使用します。 1 番目の引数として式を指定し、2 番目の引数としてその式を変換する先の型を指定します。 `DirectCast` には、2 つの引数のデータ型間の継承または実装関係が必要です。 つまり、一方の型が他方の型を継承または実装する必要があります。  
  
## <a name="errors-and-failures"></a>エラーと障害  
 `DirectCast` で、継承関係または実装関係が存在しないことが検出されると、コンパイラ エラーが発生します。 ただし、コンパイラ エラーが発生しない場合でも、変換が正常に行われるとは限りません。 目的の変換が縮小変換の場合、実行時に失敗する可能性があります。 これが発生すると、ランタイムで <xref:System.InvalidCastException> エラーがスローされます。  
  
## <a name="conversion-keywords"></a>変換キーワード  
 型変換のキーワードの比較を次に示します。  
  
|キーワード|データの種類|引数の関係|ランタイム エラー|  
|---|---|---|---|  
|[CType 関数](../functions/ctype-function.md)|任意のデータ型|2 つのデータ型の間で拡大変換または縮小変換を定義する必要があります|<xref:System.InvalidCastException> をスローする|  
|`DirectCast`|任意のデータ型|一方の型が他方の型を継承または実装する必要があります|<xref:System.InvalidCastException> をスローする|  
|[TryCast 演算子](trycast-operator.md)|参照型のみ|一方の型が他方の型を継承または実装する必要があります|[Nothing](../nothing.md) が返されます|  
  
## <a name="example"></a>例  
 次の例は、`DirectCast` の 2 つの使用方法を示しています。1 つは実行時に失敗し、もう 1 つは成功します。  
  
 [!code-vb[VbVbalrKeywords#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#1)]  
  
 前の例では、`q` の実行時の型が `Double` です。 `Double` は `Integer` に変換できるため、`CType` は成功します。 ただし、`Double` の実行時の型には `Integer` との継承関係がないため、変換が存在する場合でも、実行時に最初の `DirectCast` は失敗します。 2 番目の `DirectCast` は、型 <xref:System.Windows.Forms.Form> から型 <xref:System.Windows.Forms.Control> に変換し、そこから <xref:System.Windows.Forms.Form> が継承されるため、成功します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Convert.ChangeType%2A?displayProperty=nameWithType>
- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [暗黙の型変換と明示的な型変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
