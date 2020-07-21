---
title: '方法: オブジェクトを別の型に変換する'
ms.date: 07/20/2015
helpviewer_keywords:
- objects [Visual Basic], converting
ms.assetid: 60cb5fc7-7ba4-4ab5-9c24-480fa12ddcdc
ms.openlocfilehash: cdb78bc66867ce27076d7b7e42de6a2880cb3a8c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393962"
---
# <a name="how-to-convert-an-object-to-another-type-in-visual-basic"></a>方法: Visual Basic でオブジェクトを別の型に変換する
[CType 関数](../../../language-reference/functions/ctype-function.md)などの変換キーワードを使用して、`Object` 変数を別のデータ型に変換します。  
  
## <a name="example"></a>例  
 次の例では、`Object` 変数を `Integer` と `String` に変換します。  
  
```vb  
Public Sub objectConversion(ByVal anObject As Object)  
    Dim anInteger As Integer  
    Dim aString As String  
    anInteger = CType(anObject, Integer)  
    aString = CType(anObject, String)  
End Sub  
```  
  
 `Object` 変数の内容が特定のデータ型であることがわかっている場合は、変数をそのデータ型に変換することをお勧めします。 `Object` 変数を引き続き使用すると、"*ボックス化*" と "*ボックス化解除*" (値型の場合) または "*遅延バインディング*" (参照型の場合) のいずれかが発生します。 これらの処理にはすべて追加の実行時間がかかり、パフォーマンスが低下します。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- <xref:System?displayProperty=nameWithType> 名前空間への参照  
  
## <a name="see-also"></a>関連項目

- <xref:System.Object>
- [Visual Basic における型変換](type-conversions.md)
- [拡大変換と縮小変換](widening-and-narrowing-conversions.md)
- [暗黙の型変換と明示的な型変換](implicit-and-explicit-conversions.md)
- [文字列とその他の型との変換](conversions-between-strings-and-other-types.md)
- [配列変換](array-conversions.md)
- [構造体](structures.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)
