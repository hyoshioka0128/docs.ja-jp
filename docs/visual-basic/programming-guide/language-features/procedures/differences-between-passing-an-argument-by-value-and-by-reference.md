---
title: 引数の値渡しと参照渡しの違い
ms.date: 07/20/2015
helpviewer_keywords:
- ByRef keyword [Visual Basic], passing arguments by reference
- Visual Basic code, procedures
- procedures [Visual Basic], passing arguments
- ByVal keyword [Visual Basic], passing arguments by value
- arguments [Visual Basic], passing by value or by reference
ms.assetid: 5f5c38fe-3e2d-494c-8fff-f4025b55ec93
ms.openlocfilehash: bd316ae2239ad85e4ef6dadbb8a634d5fe7ecf02
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403331"
---
# <a name="differences-between-passing-an-argument-by-value-and-by-reference-visual-basic"></a>引数の値渡しと参照渡しの違い (Visual Basic)
プロシージャに 1 つまたは複数の引数を渡す場合、各引数は、呼び出し元のコード内の基になるプログラミング要素に対応します。 この基になる要素の値を渡すことも、それへの参照を渡すこともできます。 これは "*引渡し方法*" と呼ばれます。  
  
## <a name="passing-by-value"></a>値渡し  
 引数を "*値渡し*" するには、プロシージャ定義内の対応するパラメーターに [ByVal](../../../language-reference/modifiers/byval.md) キーワードを指定します。 この引渡し方法を使用すると、基になるプログラミング要素の値がプロシージャ内のローカル変数に Visual Basic によってコピーされます。 プロシージャコードには、呼び出し元のコード内の基になる要素へのアクセス権がありません。  
  
## <a name="passing-by-reference"></a>参照渡し  
 引数を "*参照渡し*" するには、プロシージャ定義内の対応するパラメーターに [ByRef](../../../language-reference/modifiers/byref.md) キーワードを指定します。 この引渡し方法を使用した場合、呼び出し元のコード内の基になるプログラミング要素への直接参照が Visual Basic によってプロシージャに渡されます。  
  
## <a name="passing-mechanism-and-element-type"></a>引渡し方法と要素型  
 引渡し方法を選択することは、基になる要素型を分類することと同じではありません。 値渡しまたは参照渡しでは、Visual Basic によってプロシージャ コードに提供されるものを示します。 値型または参照型では、プログラミング要素がメモリ内に格納される方法を示します。  
  
 ただし、引渡し方法と要素型は相互に関連しています。 参照型の値は、メモリ内の別の場所にあるデータを指すポインターです。 つまり、参照型を値渡しすると、プロシージャ コードには、基になる要素自体にアクセスできなくても、基になる要素のデータを指すポインターが用意されます。 たとえば、要素が配列変数である場合、プロシージャ コードから変数自体にアクセスすることはできませんが、配列のメンバーにはアクセスすることができます。  
  
## <a name="ability-to-modify"></a>変更する機能  
 変更できない要素を引数として渡した場合、その要素が `ByVal` または `ByRef` のどちらで渡されたかに関係なく、プロシージャでは呼び出し元のコード内のそれを変更することはできません。  
  
 変更可能な要素については、次の表に、要素型と引渡し方法のやり取りをまとめてあります。  
  
|要素型|`ByVal` で渡した|`ByRef` で渡した|  
|------------------|--------------------|--------------------|  
|値型 (値のみを含む)|プロシージャでは変数も、そのいずれのメンバーも変更することができません。|プロシージャでは変数とそのメンバーを変更できます。|  
|参照型 (クラスまたは構造体のインスタンスを指すポインターを含む)|プロシージャでは変数を変更することはできませんが、それによって参照されているインスタンスのメンバーを変更することはできます。|プロシージャでは変数と、それによって参照されるインスタンスのメンバーを変更できます。|  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [方法: プロシージャに引数を渡す](./how-to-pass-arguments-to-a-procedure.md)
- [引数の値渡しと参照渡し](./passing-arguments-by-value-and-by-reference.md)
- [変更できる引数と変更できない引数の違い](./differences-between-modifiable-and-nonmodifiable-arguments.md)
- [方法: プロシージャ引数の値を変更する](./how-to-change-the-value-of-a-procedure-argument.md)
- [方法: プロシージャ引数の値が変更されないように保護する](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [方法: 引数の値渡しを強制する](./how-to-force-an-argument-to-be-passed-by-value.md)
- [位置と名前による引数渡し](./passing-arguments-by-position-and-by-name.md)
- [Value Types and Reference Types](../data-types/value-types-and-reference-types.md)
