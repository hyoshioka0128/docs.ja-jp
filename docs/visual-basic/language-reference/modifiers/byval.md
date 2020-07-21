---
title: ByVal
ms.date: 07/20/2015
f1_keywords:
- vb.ByVal
- ByVal
helpviewer_keywords:
- ByVal keyword [Visual Basic], contexts
- ByVal keyword [Visual Basic]
ms.assetid: 1eaf4e58-b305-4785-9e3d-e416b9c75598
ms.openlocfilehash: c4cdafafa6bae3246c0512e28f94fde7e88d230b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84373025"
---
# <a name="byval-visual-basic"></a>ByVal (Visual Basic)
呼び出されたプロシージャまたはプロパティによって、呼び出し元のコードの引数の基になる変数の値を変更できないように、引数を[値渡し](../../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)で渡すことを指定します。 修飾子が指定されない場合、ByVal が既定になります。

> [!NOTE]
> それは既定であるため、メソッド シグネチャに `ByVal` キーワードを明示的に指定する必要はありません。 それにより、ノイズが多いコードが生成される傾向があるため、既定でない `ByRef` キーワードが見落とされることが多くなります。

## <a name="remarks"></a>Remarks
 `ByVal` 修飾子は、次のコンテキストで使用できます。

 [Declare ステートメント](../statements/declare-statement.md)

 [Function ステートメント](../statements/function-statement.md)
  
 [Operator ステートメント](../statements/operator-statement.md)
  
 [Property ステートメント](../statements/property-statement.md)
  
 [Sub ステートメント](../statements/sub-statement.md)

## <a name="example"></a>例
 次の例では、参照型の引数を指定して `ByVal` パラメーターの引き渡し方法の使用を示します。 この例では、引数は、クラス `Class1` のインスタンスである `c1` です。 `ByVal` によって、プロシージャ内のコードが参照引数 `c1` の基になる値を変更しないようになりますが、`c1` のアクセス可能なフィールドとプロパティは保護されません。

 [!code-vb[VbVbalrKeywords#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class5.vb#10)]

## <a name="see-also"></a>関連項目

- [キーワード](../keywords/index.md)
- [引数の値渡しと参照渡し](../../programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)
