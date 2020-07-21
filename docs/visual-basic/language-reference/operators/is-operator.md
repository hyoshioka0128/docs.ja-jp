---
title: Is 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.is
helpviewer_keywords:
- comparison operators [Visual Basic]
- equivalent objects
- TypeOf...Is expression
- Is operator [Visual Basic]
ms.assetid: 8045a6c8-2a83-45b6-ad47-d09a704c656d
ms.openlocfilehash: 3cc0ae5f04358fbe6b2aabc50498f39ca7225164
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370805"
---
# <a name="is-operator-visual-basic"></a>Is 演算子 (Visual Basic)
2 つのオブジェクト参照変数を比較します。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = object1 Is object2  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 任意の `Boolean` 値。  
  
 `object1`  
 必須です。 任意の `Object` 名。  
  
 `object2`  
 必須です。 任意の `Object` 名。  
  
## <a name="remarks"></a>Remarks  
 `Is` 演算子では、2 つのオブジェクト参照が同じオブジェクトを参照しているかどうかを判断します。 ただし、値の比較は行われません。 `object1` と `object2` の両方がまったく同じオブジェクト インスタンスを参照している場合、`result` は `True` です。そうでない場合、`result` は `False` です。  
  
 `Is` を `TypeOf` キーワードと共に使用して `TypeOf`...`Is` 式を作成することもできます。これにより、オブジェクト変数がデータ型に対応しているかどうかがテストされます。  
  
> [!NOTE]
> `Is` キーワードは、[Select...Case ステートメント](../statements/select-case-statement.md)でも使用されます。  
  
## <a name="example"></a>例  
 次の例では、`Is` 演算子を使用してオブジェクト参照のペアを比較します。 結果は、2 つのオブジェクトが同一かどうかを表す `Boolean` 値に割り当てられます。  
  
 [!code-vb[VbVbalrOperators#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#27)]  
  
 前の例で示したように、`Is` 演算子を使用して、事前バインディングと遅延バインディングの両方のオブジェクトをテストできます。  
  
## <a name="see-also"></a>関連項目

- [TypeOf 演算子](typeof-operator.md)
- [IsNot 演算子](isnot-operator.md)
- [Visual Basic における比較演算子](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
