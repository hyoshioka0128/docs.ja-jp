---
title: '方法: 2 つのオブジェクトが同一であるかどうかを判別する'
ms.date: 07/20/2015
helpviewer_keywords:
- testing [Visual Basic], objects
- objects [Visual Basic], comparing
- object variables [Visual Basic], determining identity
ms.assetid: 7829f817-0d1f-4749-a707-de0b95e0cf5c
ms.openlocfilehash: 67c3af8b7bdac3ad1c7e4908f1ac2684df7a87aa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410478"
---
# <a name="how-to-determine-whether-two-objects-are-identical-visual-basic"></a>方法: 2 つのオブジェクトが同一であるかどうかを判別する (Visual Basic)
Visual Basic において 2 つの変数参照は、それらのポインターが同じである場合、つまり、両方の変数がメモリ内の同じクラス インスタンスを指している場合、同一であると見なされます。 たとえば、Windows フォーム アプリケーションでは、現在のインスタンス (`Me`) が `Form2` などの特定のインスタンスと同じであるかどうかを判別するために比較を行いたい場合があります。  
  
 Visual Basic には、ポインターを比較するための演算子が 2 つ用意されています。 オブジェクトが同一である場合には、[Is 演算子](../../../language-reference/operators/is-operator.md) から `True` が返され、そうでない場合には [IsNot 演算子](../../../language-reference/operators/isnot-operator.md) から `True` が返されます。  
  
## <a name="determining-if-two-objects-are-identical"></a>2 つのオブジェクトが同一であるかどうかを判別する  
  
#### <a name="to-determine-if-two-objects-are-identical"></a>2 つのオブジェクトが同一であるかどうかを確認するには  
  
1. 2 つのオブジェクトをテストするための `Boolean` 式を設定します。  
  
2. テスト式では、2 つのオブジェクトをオペランドとする `Is` 演算子を使用します。  
  
     各オブジェクトがいずれも同じクラス インスタンスを指している場合は、`Is` から `True` が返されます。  
  
## <a name="determining-if-two-objects-are-not-identical"></a>2 つのオブジェクトが同一でないかどうかを判別する  
 2 つのオブジェクトが同一でない場合にアクションの実行が必要なことがあります。しかし、たとえば、`If Not obj1 Is obj2` のように `Not` と `Is` を組み合わせて使用するのは不便です。 そのような場合は、`IsNot` 演算子を使用できます。  
  
#### <a name="to-determine-if-two-objects-are-not-identical"></a>2 つのオブジェクトが同一でないかどうかを調べるには  
  
1. 2 つのオブジェクトをテストするための `Boolean` 式を設定します。  
  
2. テスト式では、2 つのオブジェクトをオペランドとする `IsNot` 演算子を使用します。  
  
     各オブジェクトが指しているクラス インスタンスが同じでない場合は、`IsNot` から `True` が返されます。  
  
## <a name="example"></a>例  
 次の例では、`Object` 変数のペアをテストして、それらが同じクラス インスタンスを指しているかどうかを確認します。  
  
 [!code-vb[VbVbalrKeywords#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/class7.vb#14)]  
  
 上記の例では、次の出力が表示されます。  
  
 `objA different from objB? True`  
  
 `objA identical to objC? True`  
  
## <a name="see-also"></a>関連項目

- [Object 型](../../../language-reference/data-types/object-data-type.md)
- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の値](object-variable-values.md)
- [Is 演算子](../../../language-reference/operators/is-operator.md)
- [IsNot 演算子](../../../language-reference/operators/isnot-operator.md)
- [方法: 2 つのオブジェクトが関連しているかどうかを判別する](how-to-determine-whether-two-objects-are-related.md)
- [Me、My、MyBase、および MyClass](../../program-structure/me-my-mybase-and-myclass.md)
