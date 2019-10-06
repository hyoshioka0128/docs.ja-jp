---
title: '方法: Visual Basic の StringBuilder を使用して文字列を作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- StringBuilder class
- strings [Visual Basic], using StringBuilder
ms.assetid: 9c042880-aa16-432e-9ccb-cd00abda9ae3
ms.openlocfilehash: 19e036abc9d25ec7fdfd6c33ebb420ec4f503cbc
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700103"
---
# <a name="how-to-create-strings-using-a-stringbuilder-in-visual-basic"></a>方法: Visual Basic の StringBuilder を使用して文字列を作成する

この例では、<xref:System.Text.StringBuilder> クラスを使用して、多数の小さい文字列から長い文字列を構築します。 @No__t-0 クラスは、多数の文字列を連結するための `&=` 演算子よりも効率的です。

## <a name="example"></a>例

次の例では、@no__t 0 クラスのインスタンスを作成し、そのインスタンスに1000文字列を追加して、その文字列形式を返します。

 [!code-vb[VbVbalrStrings#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#70)]

## <a name="see-also"></a>関連項目

- [StringBuilder クラスの使用](../../../../standard/base-types/stringbuilder.md)
- [& = 演算子](../../../language-reference/operators/and-assignment-operator.md)
- [文字列](index.md)
- [新しい文字列の作成](../../../../standard/base-types/creating-new.md)
- [文字列の操作](../../../../standard/base-types/manipulating-strings.md)
