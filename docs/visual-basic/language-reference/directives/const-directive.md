---
title: '#Const ディレクティブ'
ms.date: 07/20/2015
f1_keywords:
- vb.#Const
- '#vb.Const'
- '#Const'
helpviewer_keywords:
- '#Const directive'
- conditional compilation [Visual Basic], directives
- Const directive (#Const)
- Visual Basic compiler, compiler directives
- constants [Visual Basic], Const directive
- constants [Visual Basic], declaring
- Const statement [Visual Basic], directive (#Const)
- 'declaring constants [Visual Basic], #const directive'
ms.assetid: 707669e5-23f9-4f17-8622-a0d534429386
ms.openlocfilehash: 91152771a4ef5ec74a7408511ccc2afe28dd442e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415467"
---
# <a name="const-directive"></a>#Const ディレクティブ

Visual Basic の条件付きコンパイラ定数を定義します。  
  
## <a name="syntax"></a>構文  
  
```vb  
#Const constname = expression  
```  
  
## <a name="parts"></a>指定項目  

 `constname`  
 必須です。 定義している定数の名前。  
  
 `expression`  
 必須です。 リテラル、他の条件付きコンパイラ定数、または、`Is` 以外の算術演算子または論理演算子のいずれか、またはすべてを含む任意の組み合わせ。  
  
## <a name="remarks"></a>Remarks  

 条件付きコンパイラ定数は、それらが出現するファイルに対して常にプライベートです。 `#Const` ディレクティブを使用して、パブリック コンパイラ定数を作成することはできません。これらは、ユーザー インターフェイス内、または `/define` コンパイラ オプションを使用する場合にのみ作成できます。  
  
 `expression` では、条件付きコンパイラ定数とリテラルのみを使用できます。 `Const` で定義された標準定数を使用すると、エラーが発生します。 逆に、`#Const` キーワードによって定義された定数は、条件付きコンパイルにのみ使用できます。 定数を未定義にすることもできます。その場合、値は `Nothing` になります。  
  
## <a name="example"></a>例  

 `#Const` ディレクティブの使用例を次に示します。  
  
 [!code-vb[VbVbalrConditionalComp#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [-define (Visual Basic)](../../reference/command-line-compiler/define.md)
- [#If...Then...#Else ディレクティブ](if-then-else-directives.md)
- [Const ステートメント](../statements/const-statement.md)
- [条件付きコンパイル](../../programming-guide/program-structure/conditional-compilation.md)
- [If...Then...Else ステートメント](../statements/if-then-else-statement.md)
