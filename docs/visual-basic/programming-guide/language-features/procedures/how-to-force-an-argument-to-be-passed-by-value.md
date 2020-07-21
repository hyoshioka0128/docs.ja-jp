---
title: '方法: 引数の値渡しを強制する'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- procedures [Visual Basic], calling
- arguments [Visual Basic], in parentheses
- procedure arguments [Visual Basic], in parentheses
- arguments [Visual Basic], changing value
ms.assetid: 77b4f2d2-1055-4c2f-a521-874d1db86946
ms.openlocfilehash: 48f7d7afebd76916cba11459532d89d71871c79b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387986"
---
# <a name="how-to-force-an-argument-to-be-passed-by-value-visual-basic"></a>方法: 引数の値渡しを強制する (Visual Basic)
プロシージャ宣言によって引渡し方法が決まります。 Visual Basic では、パラメーターが [ByRef](../../../language-reference/modifiers/byref.md) として宣言されている場合、対応する引数は参照渡しになります。 これにより、プロシージャは引数の基になる呼び出し元のコードのプログラミング要素の値を変更できます。 基になる要素をこのような変更から保護する場合は、引数名をかっこで囲むことで、プロシージャ呼び出しの引渡し方法 `ByRef` をオーバーライドできます。 これらのかっこは、呼び出しの引数リストを囲むかっこに追加されます。  
  
 呼び出し元のコードでは、引渡し方法 [ByVal](../../../language-reference/modifiers/byval.md) をオーバーライドできません。  
  
### <a name="to-force-an-argument-to-be-passed-by-value"></a>引数の値渡しを強制するには  
  
- 対応するパラメーターがプロシージャで `ByVal` として宣言されている場合は、追加の手順を実行する必要はありません。 引数は既に値渡しになっています。  
  
- 対応するパラメーターがプロシージャで `ByRef` として宣言されている場合は、プロシージャ呼び出しで引数をかっこで囲みます。  
  
## <a name="example"></a>例  
 次の例では、`ByRef` パラメーター宣言をオーバーライドします。 `ByVal` を強制する呼び出しでは、2 つのレベルのかっこがあることに注意してください。  
  
 [!code-vb[VbVbcnProcedures#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#39)]  
  
 [!code-vb[VbVbcnProcedures#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#40)]  
  
 引数リスト内で `str` が追加のかっこで囲まれている場合、`setNewString` プロシージャは呼び出し元のコードの値を変更できず、`MsgBox` に "Cannot be replaced if passed ByVal (ByVal で渡した場合、置き換えることはできません)" と表示されます。 `str` が追加のかっこで囲まれていない場合、プロシージャは値を変更することができ、`MsgBox` に "This is a new value for the inString argument (これは inString 引数の新しい値です)" と表示されます。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 変数を参照渡しにするときは、`ByRef` キーワードを使用してこの方法を指定する必要があります。  
  
 Visual Basic の既定では、引数は値渡しになります。 ただし、宣言されるすべてのパラメーターに、[ByVal](../../../language-reference/modifiers/byval.md) または [ByRef](../../../language-reference/modifiers/byref.md) キーワードを含めることをお勧めします。 これにより、コードが読みやすくなります。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 プロシージャでパラメーターが [ByRef](../../../language-reference/modifiers/byref.md) として宣言されている場合、コードの正しい実行は、呼び出し元のコードの基になる要素を変更できるかどうかに左右されます。 呼び出し元のコードで、引数をかっこで囲んでこの引渡し方法をオーバーライドした場合や、変更不可能な引数を渡した場合、プロシージャは基になる要素を変更できません。 これにより、呼び出し元のコードで予期しない結果が生じる可能性があります。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 プロシージャが呼び出し元のコードの引数の基になる値を変更できるようにする場合、常に潜在的なリスクがあります。 この値が変更されることを想定し、使用前に有効性をチェックする準備をしておく必要があります。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [変更できる引数と変更できない引数の違い](./differences-between-modifiable-and-nonmodifiable-arguments.md)
- [引数の値渡しと参照渡しの違い](./differences-between-passing-an-argument-by-value-and-by-reference.md)
- [方法: プロシージャ引数の値を変更する](./how-to-change-the-value-of-a-procedure-argument.md)
- [方法: プロシージャ引数の値が変更されないように保護する](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [位置と名前による引数渡し](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../data-types/value-types-and-reference-types.md)
