---
title: '方法: StringBuilder を使用して文字列を作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- StringBuilder class
- strings [Visual Basic], using StringBuilder
ms.assetid: 9c042880-aa16-432e-9ccb-cd00abda9ae3
ms.openlocfilehash: c41db584df83782dab99b90043045aa2cabcb6ff
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81645325"
---
# <a name="how-to-create-strings-using-a-stringbuilder-in-visual-basic"></a>方法: Visual Basic の StringBuilder を使用して文字列を作成する

この例では、<xref:System.Text.StringBuilder> クラスを使用して、多数の短い文字列から長い文字列を作成します。 多数の文字列を連結する場合、<xref:System.Text.StringBuilder> クラスは `&=` 演算子よりも効率的です。

## <a name="example"></a>例

次の例では、<xref:System.Text.StringBuilder> クラスのインスタンスを作成し、そのインスタンスに 1,000 個の文字列を追加した後、その文字列表現を返します。

 [!code-vb[VbVbalrStrings#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#70)]

## <a name="see-also"></a>関連項目

- [StringBuilder クラスの使用](../../../../standard/base-types/stringbuilder.md)
- [& = 演算子](../../../language-reference/operators/and-assignment-operator.md)
- [文字列](index.md)
- [新しい文字列の作成](../../../../standard/base-types/creating-new.md)
- [文字列の操作](../../../../standard/base-types/best-practices-strings.md)
