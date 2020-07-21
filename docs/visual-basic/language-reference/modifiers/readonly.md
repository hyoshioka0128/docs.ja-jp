---
title: ReadOnly
ms.date: 07/20/2015
f1_keywords:
- vb.ReadOnly
helpviewer_keywords:
- ReadOnly keyword [Visual Basic]
- variables [Visual Basic], read-only
- ReadOnly property
- properties [Visual Basic], read-only
- read-only variables
ms.assetid: e868185d-6142-4359-a2fd-a7965cadfce8
ms.openlocfilehash: 405297a25d4b948a6920bd989c7826e8b6f66bb4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398208"
---
# <a name="readonly-visual-basic"></a>ReadOnly (Visual Basic)
変数またはプロパティを読み込めるが、書き込みはできないことを示します。

## <a name="remarks"></a>Remarks

## <a name="rules"></a>ルール

- **宣言コンテキスト。** `ReadOnly` は、モジュール レベルでのみ使用できます。 つまり、`ReadOnly` 要素の宣言コンテキストは、クラス、構造体、またはモジュールにする必要があり、ソース ファイル、名前空間、またはプロシージャにすることはできません。

- **結合された修飾子。** 同じ宣言内で `ReadOnly` を `Static` と共に指定することはできません。

- **値の代入。** `ReadOnly` プロパティを使用するコードでは、その値を設定できません。 ただし、基になるストレージにアクセスできるコードは、いつでも値を代入したり変更したりできます。

     `ReadOnly` 変数に値を代入できるのは、その宣言内、またはそれが定義されているクラスまたは構造体のコンストラクター内でのみです。

## <a name="when-to-use-a-readonly-variable"></a>ReadOnly 変数を使用するタイミング

定数値の宣言と割り当てに [Const ステートメント](../statements/const-statement.md) を使用できない場合があります。 たとえば、`Const` ステートメントが割り当てたいデータ型を受け入れない場合や、コンパイル時に定数式を使用して値を計算できない場合があります。 コンパイル時に値がわからない場合もあります。 このような場合は、`ReadOnly` 変数を使用して定数値を保持できます。

> [!IMPORTANT]
> 変数のデータ型が配列やクラス インスタンスなどの参照型である場合は、変数自体が `ReadOnly` の場合でも、そのメンバーを変更できます。 次に例を示します。

```vb
ReadOnly characterArray() As Char = {"x"c, "y"c, "z"c}
Sub ChangeArrayElement()
    characterArray(1) = "M"c
End Sub
```

初期化されると、`characterArray()` が指す配列は、"x"、"y"、および "z" を保持します。 変数 `characterArray` が `ReadOnly` であるため、初期化後にその値を変更することはできません。つまり、新しい配列を割り当てることはできません。 ただし、1 つまたは複数の配列メンバーの値を変更できます。 プロシージャ `ChangeArrayElement` の呼び出しの後、`characterArray()` が指す配列は "x"、"M"、および "z" を保持します。

これは、プロシージャ パラメーターを [ByVal](byval.md) として宣言するのと似ています。これにより、プロシージャは呼び出し元の引数自体を変更できなくなりますが、メンバーを変更できるようになります。

## <a name="example"></a>例

次の例では、従業員が採用された日付の `ReadOnly` プロパティを定義します。 クラスはプロパティ値を `Private` 変数として内部的に格納し、クラス内のコードだけがその値を変更できます。 ただし、プロパティは `Public` であり、クラスにアクセスできるすべてのコードでプロパティを読み取ることができます。

[!code-vb[VbVbalrKeywords#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class1.vb#4)]

`ReadOnly` 修飾子は、次のコンテキストで使用できます。

- [Dim ステートメント](../statements/dim-statement.md)
- [Property ステートメント](../statements/property-statement.md)

## <a name="see-also"></a>関連項目

- [WriteOnly](writeonly.md)
- [キーワード](../keywords/index.md)
