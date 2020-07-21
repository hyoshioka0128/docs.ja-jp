---
title: ParamArray
ms.date: 07/20/2015
f1_keywords:
- vb.ParamArray
- ParamArray
helpviewer_keywords:
- ParamArray keyword [Visual Basic]
- ParamArray keyword [Visual Basic], syntax
ms.assetid: a5f18789-92bd-488f-9c7e-cf3719963635
ms.openlocfilehash: e3c24818ea87884a0dd9b42c604e13e16ca6d3d7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84391821"
---
# <a name="paramarray-visual-basic"></a>ParamArray (Visual Basic)
プロシージャのパラメーターが、指定された型の、省略可能な要素の配列を受け取ることを示します。 `ParamArray` は、パラメーター リストの最後のパラメーターでのみ使用できます。  
  
## <a name="remarks"></a>Remarks  
 `ParamArray` により、プロシージャに任意の数の引数を渡すことができます。 `ParamArray` パラメーターは常に、[ByVal](byval.md) を使用して宣言します。  
  
 適切なデータ型の配列やコンマ区切りの値のリストを渡すか、または何も渡さないで、`ParamArray` パラメーターに 1 つ以上の引数を指定することができます。 詳細については、「[パラメーター配列](../../programming-guide/language-features/procedures/parameter-arrays.md)」の「ParamArray の呼び出し」を参照してください。  
  
> [!IMPORTANT]
> 無限に大きくなる可能性がある配列を処理する場合は常に、アプリケーションの何らかの内部容量が超過するリスクがあります。 呼び出し元のコードからパラメーター配列を受け取る場合は、その長さをテストし、それがアプリケーションに大きすぎる場合は、適切なステップを実行する必要があります。  
  
 `ParamArray` 修飾子は、次のコンテキストで使用できます。  
  
 [Declare ステートメント](../statements/declare-statement.md)  
  
 [Function ステートメント](../statements/function-statement.md)  
  
 [Property ステートメント](../statements/property-statement.md)  
  
 [Sub ステートメント](../statements/sub-statement.md)  
  
## <a name="see-also"></a>関連項目

- [キーワード](../keywords/index.md)
- [パラメーター配列](../../programming-guide/language-features/procedures/parameter-arrays.md)
