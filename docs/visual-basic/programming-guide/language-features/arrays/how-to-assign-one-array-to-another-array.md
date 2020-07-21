---
title: '方法: 配列を別の配列に代入する'
ms.date: 07/20/2015
helpviewer_keywords:
- covariance, arrays
- arrays [Visual Basic], assigning
- arrays [Visual Basic], covariance
ms.assetid: 1ae89ea5-f292-4282-bcfc-e9b06b37fbd5
ms.openlocfilehash: c38def1ba9f3720bc760d6f6e4264510c884c930
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413080"
---
# <a name="how-to-assign-one-array-to-another-array-visual-basic"></a>方法: 配列を別の配列に代入する (Visual Basic)

配列はオブジェクトであるため、他のオブジェクト型と同様に代入ステートメントで使用できます。 配列変数に保持されるのは、配列要素と、ランクおよび長さの情報で構成されるデータへのポインターで、このポインターのみが代入によってコピーされます。

### <a name="to-assign-one-array-to-another-array"></a>配列を別の配列に代入するには

1. 2 つの配列両方が同じランク (次元数) であり、互換性のある要素データ型を持つことを確認します。

2. 標準の代入ステートメントを使用して、ソース配列を宛先配列に代入します。 どちらの配列名も、後ろにかっこをつけないでください。

    ```vb
    Dim formArray() As System.Windows.Forms.Form
    Dim controlArray() As System.Windows.Forms.Control
    controlArray = formArray
    ```

配列を別の配列に代入するときは、次の規則が適用されます。

- **ランクが同じ。** 宛先配列のランク (次元数) は、ソース配列のランクと同じでなければなりません。

  2 つの配列のランクが等しいことが必要であって、次元は同じである必要はありません。 特定の次元の要素の数は、代入時に変更される場合があります。

- **要素型**。 両方の配列が "*参照型*" 要素を持つか、または両方の配列が "*値型*" 要素を持つ必要があります。 詳細については、「 [Value Types and Reference Types](../data-types/value-types-and-reference-types.md)」を参照してください。

  - 両方の配列が値型の要素を持つ場合、要素のデータ型はまったく同じでなければなりません。 ただし、`Enum` 要素の配列を、その `Enum` の基本データ型の配列に代入できる場合を除きます。

  - 両方の配列が参照型要素を持つ場合、ソース要素の型は、宛先要素型から派生している必要があります。 この場合、2 つの配列の継承関係は、その要素と同じです。 これは "*配列の共変性*" と呼ばれます。

上記の規則に違反している場合、たとえば、データ型に互換性がなかったり、ランクが等しくなかったりすると、コンパイラによってエラーが報告されます。 コードにエラー処理を追加すると、代入を試みる前に配列に互換性があることを確認できます。 [TryCast 演算子](../../../language-reference/operators/trycast-operator.md)キーワードを使って、例外がスローされないようにすることもできます。

## <a name="see-also"></a>関連項目

- [配列](index.md)
- [配列のトラブルシューティング](troubleshooting-arrays.md)
- [Enum ステートメント](../../../language-reference/statements/enum-statement.md)
- [配列変換](../data-types/array-conversions.md)
