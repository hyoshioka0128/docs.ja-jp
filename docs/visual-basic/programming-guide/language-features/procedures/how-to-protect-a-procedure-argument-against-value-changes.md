---
title: '方法: プロシージャ引数の値が変化しないようにする'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- arguments [Visual Basic], passing by reference
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- procedures [Visual Basic], calling
- arguments [Visual Basic], ByRef
- arguments [Visual Basic], changing value
ms.assetid: d2b7c766-ce16-4d2c-8d79-3fc0e7ba2227
ms.openlocfilehash: b0504d9f7a8862274d5d71dc6a9c1570551629a5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414364"
---
# <a name="how-to-protect-a-procedure-argument-against-value-changes-visual-basic"></a>方法: プロシージャ引数の値が変更されないように保護する (Visual Basic)
Visual Basic では、プロシージャでパラメーターが [ByRef](../../../language-reference/modifiers/byref.md) として宣言されている場合、引数の基になる呼び出し元のコードのプログラミング要素への直接参照がプロシージャ コードに渡されます。 これにより、プロシージャは引数の基になる呼び出し元のコードの値を変更できます。 呼び出し元のコードで、そのような変更から保護することが必要な場合もあります。  
  
 プロシージャで対応するパラメーターを [ByVal](../../../language-reference/modifiers/byval.md) として宣言することで、引数を変更から常に保護できます。 特定の引数を一部のケースでは変更できるようにし、他のケースでは変更できないようにする場合は、その引数を `ByRef` として宣言し、呼び出し元のコードが呼び出しごとに引渡し方法を決定できるようにします。 これを行うには、対応する引数をかっこで囲んで値渡しにするか、かっこで囲まずに参照渡しにします。 詳細については、[方法: 引数の値渡しを強制する](./how-to-force-an-argument-to-be-passed-by-value.md)」をご覧ください。  
  
## <a name="example"></a>例  
 次の例は、配列変数を受け取り、その要素を操作する 2 つのプロシージャを示しています。 `increase` プロシージャは、各要素に 1 を加算するだけです。 `replace` プロシージャは、`a()` パラメーターに新しい配列を割り当ててから、各要素に 1 を加算します。 ただし、再割り当ては、呼び出し元のコードの基になる配列変数には影響しません。  
  
 [!code-vb[VbVbcnProcedures#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#35)]  
  
 [!code-vb[VbVbcnProcedures#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#38)]  
  
 [!code-vb[VbVbcnProcedures#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#37)]  
  
 最初の `MsgBox` 呼び出しでは、"After increase(n): 11, 21, 31, 41" と表示されます。 配列 `n` は参照型であるため、引渡し方法が `ByVal` であっても、`increase` はそのメンバーを変更できます。  
  
 2 番目の `MsgBox` 呼び出しでは、"After replace(n): 11, 21, 31, 41" と表示されます。 `n` は `ByVal` で渡されるため、`replace` は呼び出し元のコードの変数 `n` に新しい配列を割り当てて変更することはできません。 `replace` が新しい配列インスタンス `k` を作成し、ローカル変数 `a` に割り当てると、呼び出し元のコードによって渡された `n` への参照は失われます。 `a` のメンバーを変更すると、ローカル配列 `k` だけが影響を受けます。 したがって、`replace` は呼び出し元のコードの配列 `n` の値をインクリメントしません。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 Visual Basic の既定では、引数は値渡しになります。 ただし、宣言されるすべてのパラメーターに、[ByVal](../../../language-reference/modifiers/byval.md) または [ByRef](../../../language-reference/modifiers/byref.md) キーワードを含めることをお勧めします。 これにより、コードが読みやすくなります。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [変更できる引数と変更できない引数の違い](./differences-between-modifiable-and-nonmodifiable-arguments.md)
- [引数の値渡しと参照渡しの違い](./differences-between-passing-an-argument-by-value-and-by-reference.md)
- [方法: プロシージャ引数の値を変更する](./how-to-change-the-value-of-a-procedure-argument.md)
- [方法: 引数の値渡しを強制する](./how-to-force-an-argument-to-be-passed-by-value.md)
- [位置と名前による引数渡し](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../data-types/value-types-and-reference-types.md)
