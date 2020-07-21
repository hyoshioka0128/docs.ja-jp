---
title: TryCast 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.trycast
- trycast
helpviewer_keywords:
- TryCast keyword [Visual Basic]
ms.assetid: d1ef5d47-fef4-491e-b014-1d910628f65c
ms.openlocfilehash: 8f0d4f612cd5a96e0b0ab7305c41e00790613cc8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406388"
---
# <a name="trycast-operator-visual-basic"></a>TryCast 演算子 (Visual Basic)
例外をスローしない型変換操作を導入します。  
  
## <a name="remarks"></a>Remarks  
 試行された変換が失敗した場合、`CType` と `DirectCast` はどちらも <xref:System.InvalidCastException> エラーをスローします。 これは、アプリケーションのパフォーマンスに悪影響を与える可能性があります。 `TryCast` は [Nothing](../nothing.md) を返します。そのため、発生する可能性がある例外を処理する必要はなく、代わりに、返された結果を `Nothing` に対してテストすることのみ必要です。  
  
 `TryCast` キーワードは、[CType 関数](../functions/ctype-function.md)および [DirectCast 演算子](directcast-operator.md)キーワードを使用するのと同じ方法で使用します。 1 番目の引数として式を指定し、2 番目の引数としてその式の変換先の型を指定します。 `TryCast` は、クラスやインターフェイスなどの参照型に対してのみ動作します。 2 つの型間の継承関係または実装関係が必要になります。 つまり、一方の型が他方の型を継承または実装する必要があります。  
  
## <a name="errors-and-failures"></a>エラーと障害  
 `TryCast` で、継承関係または実装関係が存在しないことが検出されると、コンパイラ エラーが発生します。 ただし、コンパイラ エラーが発生しない場合でも、変換が正常に行われるとは限りません。 目的の変換が縮小変換の場合、実行時に失敗する可能性があります。 これが発生すると、`TryCast` は [Nothing](../nothing.md) を返します。  
  
## <a name="conversion-keywords"></a>変換キーワード  
 型変換のキーワードの比較を次に示します。  
  
|キーワード|データの種類|引数の関係|ランタイム エラー|  
|---|---|---|---|  
|[CType 関数](../functions/ctype-function.md)|任意のデータ型|2 つのデータ型の間で拡大変換または縮小変換を定義する必要があります|<xref:System.InvalidCastException> がスローされます|  
|[DirectCast 演算子](directcast-operator.md)|任意のデータ型|一方の型が他方の型を継承または実装する必要があります|<xref:System.InvalidCastException> がスローされます|  
|`TryCast`|参照型のみ|一方の型が他方の型を継承または実装する必要があります|[Nothing](../nothing.md) が返されます|  
  
## <a name="example"></a>例  
 次の例は、`TryCast` を使用する方法を示しています。  
  
 [!code-vb[VbVbalrKeywords#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>関連項目

- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [暗黙の型変換と明示的な型変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
