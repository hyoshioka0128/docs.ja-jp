---
title: 引数の値渡しと参照渡し
ms.date: 07/20/2015
helpviewer_keywords:
- ByRef keyword [Visual Basic], passing arguments by reference
- Visual Basic code, procedures
- passing arguments [Visual Basic], by value or by reference
- ByVal keyword [Visual Basic], passing arguments by value
- arguments [Visual Basic], passing by value or by reference
- argument passing [Visual Basic], by value or by reference
ms.assetid: fd8a9de6-7178-44d5-a9bf-458d4ad907c2
ms.openlocfilehash: 3dd4be6ea6de9dfe8eb165e5d4ba9a990fc40585
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363955"
---
# <a name="passing-arguments-by-value-and-by-reference-visual-basic"></a>引数の値渡しと参照渡し (Visual Basic)
Visual Basic では、プロシージャに引数を渡すときに、"*値*" 渡しまたは "*参照*" 渡しにすることができます。 これは "*引渡し方法*" と呼ばれ、引数の基になる呼び出し元のコードのプログラミング要素をプロシージャが変更できるかどうかを決定します。 プロシージャの宣言で [ByVal](../../../language-reference/modifiers/byval.md) または [ByRef](../../../language-reference/modifiers/byref.md) キーワードを指定することによって、各パラメーターの引渡し方法を決定します。  
  
## <a name="distinctions"></a>相違点  
 プロシージャに引数を渡すときは、相互作用するいくつかの相違点に注意してください。  
  
- 基になるプログラミング要素が変更可能か変更不可能か  
  
- 引数自体が変更可能か変更不可能か  
  
- 引数が値渡しか参照渡しか  
  
- 引数のデータ型が値型か参照型か  
  
 詳細については、「[Differences Between Modifiable and Nonmodifiable Arguments (変更できる引数と変更できない引数の違い)](./differences-between-modifiable-and-nonmodifiable-arguments.md)」および「[Differences Between Passing an Argument By Value and By Reference (引数の値渡しと参照渡しの違い)](./differences-between-passing-an-argument-by-value-and-by-reference.md)」をご覧ください。  
  
## <a name="choice-of-passing-mechanism"></a>引渡し方法の選択  
 引数ごとに引渡し方法を慎重に選択する必要があります。  
  
- **保護**。 2 つの引渡し方法のいずれかを選択する際に、最も重要な基準は、呼び出し元の変数が変更の影響を受けるかどうかです。 引数を `ByRef` で渡す利点は、プロシージャがその引数を使用して呼び出し元のコードに値を返すことができることです。 引数を `ByVal` で渡す利点は、プロシージャによって変更されないように変数を保護することです。  
  
- **パフォーマンス**。 引渡し方法はコードのパフォーマンスに影響を与える可能性がありますが、通常、その違いはわずかです。 唯一の例外は、`ByVal` で渡される値型です。 この場合、Visual Basic では引数のデータ コンテンツ全体をコピーします。 そのため、構造体などの大きな値型の場合、`ByRef` で渡す方が効率的です。  
  
     参照型の場合、データへのポインターだけがコピーされます (32 ビット プラットフォームでは 4 バイト、64 ビット プラットフォームでは 8 バイト)。 そのため、パフォーマンスを損なうことなく、`String` または `Object` 型の引数を値渡しにすることができます。  
  
## <a name="determination-of-the-passing-mechanism"></a>引渡し方法の決定  
 プロシージャの宣言で、各パラメーターの引渡し方法を指定します。 呼び出し元のコードは、引渡し方法 `ByVal` をオーバーライドできません。  
  
 パラメーターが `ByRef` で宣言されている場合、呼び出し元のコードは、呼び出しで引数名をかっこで囲むことによって、引渡し方法を強制的に `ByVal` にすることができます。 詳細については、「[方法:方法: 引数の値渡しを強制する](./how-to-force-an-argument-to-be-passed-by-value.md)」をご覧ください。  
  
 Visual Basic の既定では、引数は値渡しになります。  
  
## <a name="when-to-pass-an-argument-by-value"></a>引数を値渡しにする場合  
  
- 引数の基になる呼び出し元のコードの要素が変更不可能な要素である場合は、対応するパラメーターを [ByVal](../../../language-reference/modifiers/byval.md) で宣言します。 コードは、変更不可能な要素の値を変更することはできません。  
  
- 基になる要素が変更可能であっても、プロシージャがその値を変更できないようにする場合は、パラメーターを `ByVal` で宣言します。 値渡しされた変更可能な要素の値を変更できるのは、呼び出し元のコードだけです。  
  
## <a name="when-to-pass-an-argument-by-reference"></a>引数を参照渡しにする場合  
  
- プロシージャが呼び出し元のコードの基になる要素を変更する必要がある場合は、対応するパラメーターを [ByRef](../../../language-reference/modifiers/byref.md) で宣言します。  
  
- コードを正しく実行するには、呼び出し元のコードの基になる要素をプロシージャが変更する必要がある場合は、パラメーターを `ByRef` で宣言します。 値渡しにした場合や、呼び出し元のコードで引数をかっこで囲むことによって引渡し方法 `ByRef` をオーバーライドした場合、プロシージャ呼び出しによって予期しない結果が生じる可能性があります。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例は、引数を値渡しにする場合と参照渡しにする場合を示しています。 `Calculate` プロシージャには、`ByVal` パラメーターと `ByRef` パラメーターの両方があります。 このプロシージャのタスクは、指定された `rate` (金利) と `debt` (合計金額) を使用して、`debt` の新しい値を計算することです。これは、`debt` の元の値に金利を適用した結果です。 `debt` は `ByRef` パラメーターであるため、新しい合計は、`debt` に対応する呼び出し元のコードの引数の値に反映されます。 `Calculate` が値を変更しないようにする必要があるため、`rate` パラメーターは `ByVal` パラメーターです。  
  
### <a name="code"></a>コード  
 [!code-vb[VbVbcnProcedures#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class2.vb#74)]  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [方法: プロシージャ引数の値を変更する](./how-to-change-the-value-of-a-procedure-argument.md)
- [方法: プロシージャ引数の値が変更されないように保護する](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [方法: 引数の値渡しを強制する](./how-to-force-an-argument-to-be-passed-by-value.md)
- [位置と名前による引数渡し](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../data-types/value-types-and-reference-types.md)
