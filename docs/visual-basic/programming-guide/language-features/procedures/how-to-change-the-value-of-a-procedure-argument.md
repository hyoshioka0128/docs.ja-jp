---
title: '方法: プロシージャ引数の値を変更する'
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
- arguments [Visual Basic], ByRef
- arguments [Visual Basic], changing value
ms.assetid: 6fad2368-5da7-4c07-8bf8-0f4e65a1be67
ms.openlocfilehash: 46cf9062d01e248b6e90882a923a48210780f7f4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388505"
---
# <a name="how-to-change-the-value-of-a-procedure-argument-visual-basic"></a>方法: プロシージャ引数の値を変更する (Visual Basic)
プロシージャを呼び出すときに、指定する引数は、プロシージャで定義されているパラメーターにそれぞれ対応しています。 プロシージャ コードが、呼び出し元のコードの引数の基になる値を変更できる場合があります。 また、プロシージャが引数のローカル コピーのみを変更できる場合もあります。  
  
 Visual Basic では、プロシージャを呼び出すときに、[ByVal](../../../language-reference/modifiers/byval.md) で渡されるすべての引数のローカル コピーが作成されます。 [ByRef](../../../language-reference/modifiers/byref.md) で渡される各引数では、引数の基になる呼び出し元のコードのプログラミング要素への直接参照がプロシージャ コードに渡されます。  
  
 呼び出し元のコードの基になる要素が変更可能な要素であり、引数が `ByRef` で渡される場合、プロシージャ コードは直接参照を使用して呼び出し元のコードの要素の値を変更できます。  
  
## <a name="changing-the-underlying-value"></a>基になる値を変更する  
  
#### <a name="to-change-the-underlying-value-of-a-procedure-argument-in-the-calling-code"></a>呼び出し元のコードのプロシージャ引数の基になる値を変更するには  
  
1. プロシージャの宣言で、引数に対応するパラメーターに [ByRef](../../../language-reference/modifiers/byref.md) を指定します。  
  
2. 呼び出し元のコードで、変更可能なプログラミング要素を引数として渡します。  
  
3. 呼び出し元のコードでは、引数リストの引数をかっこで囲まないでください。  
  
4. プロシージャ コードで、パラメーター名を使用して、呼び出し元のコードの基になる要素に値を割り当てます。  
  
 デモについては、後述の例を参照してください。  
  
## <a name="changing-local-copies"></a>ローカル コピーを変更する  
 呼び出し元のコードの基になる要素が変更不可能な要素である場合や、引数が `ByVal` で渡される場合、プロシージャは呼び出し元のコードの値を変更することはできません。 ただし、プロシージャはそのような引数のローカル コピーを変更できます。  
  
#### <a name="to-change-the-copy-of-a-procedure-argument-in-the-procedure-code"></a>プロシージャ コードのプロシージャ引数のコピーを変更するには  
  
1. プロシージャの宣言で、引数に対応するパラメーターに [ByVal](../../../language-reference/modifiers/byval.md) を指定します。  
  
     \- または -  
  
     呼び出し元のコードで、引数リストの引数をかっこで囲みます。 これにより、対応するパラメーターに `ByRef` が指定されている場合でも、引数の値渡しが強制されます。  
  
2. プロシージャ コードで、パラメーター名を使用して、引数のローカル コピーに値を割り当てます。 呼び出し元のコードの基になる値は変更されません。  
  
## <a name="example"></a>例  
 次の例は、配列変数を受け取り、その要素を操作する 2 つのプロシージャを示しています。 `increase` プロシージャは、各要素に 1 を加算するだけです。 `replace` プロシージャは、`a()` パラメーターに新しい配列を割り当ててから、各要素に 1 を加算します。  
  
 [!code-vb[VbVbcnProcedures#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#35)]  
  
 [!code-vb[VbVbcnProcedures#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#36)]  
  
 [!code-vb[VbVbcnProcedures#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#37)]  
  
 最初の `MsgBox` 呼び出しでは、"After increase(n): 11, 21, 31, 41" と表示されます。 配列 `n` は参照型であるため、引渡し方法が `ByVal` であっても、`replace` はそのメンバーを変更できます。  
  
 2 番目の `MsgBox` 呼び出しでは、"After replace(n): 101, 201, 301" と表示されます。 `n` は `ByRef` で渡されるため、`replace` は呼び出し元のコードの変数 `n` を変更して新しい配列を割り当てることができます。 `n` は参照型であるため、`replace` はそのメンバーを変更することもできます。  
  
 プロシージャが、呼び出し元のコードの変数自体を変更できないようにすることができます。 「[方法:プロシージャ引数の値が変更されないように保護する](./how-to-protect-a-procedure-argument-against-value-changes.md)」をご覧ください。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 変数を参照渡しにするときは、`ByRef` キーワードを使用してこの方法を指定する必要があります。  
  
 Visual Basic の既定では、引数は値渡しになります。 ただし、宣言されるすべてのパラメーターに、[ByVal](../../../language-reference/modifiers/byval.md) または [ByRef](../../../language-reference/modifiers/byref.md) キーワードを含めることをお勧めします。 これにより、コードが読みやすくなります。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 プロシージャが呼び出し元のコードの引数の基になる値を変更できるようにする場合、常に潜在的なリスクがあります。 この値が変更されることを想定し、使用前に有効性をチェックする準備をしておく必要があります。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [変更できる引数と変更できない引数の違い](./differences-between-modifiable-and-nonmodifiable-arguments.md)
- [引数の値渡しと参照渡しの違い](./differences-between-passing-an-argument-by-value-and-by-reference.md)
- [方法: プロシージャ引数の値が変更されないように保護する](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [方法: 引数の値渡しを強制する](./how-to-force-an-argument-to-be-passed-by-value.md)
- [位置と名前による引数渡し](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../data-types/value-types-and-reference-types.md)
