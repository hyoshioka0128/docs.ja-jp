---
title: 構造体の変数
ms.date: 07/20/2015
helpviewer_keywords:
- structures [Visual Basic], variables
- structures [Visual Basic], structure variables
- variables [Visual Basic], structure variables
- structure variables [Visual Basic]
ms.assetid: 156872f8-aabc-4454-8e2d-f2253c3c13c9
ms.openlocfilehash: 270e8ca26185e4a68def3b95f4ce6ab4c57a629c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393586"
---
# <a name="structure-variables-visual-basic"></a>構造体の変数 (Visual Basic)

構造体を作成したら、プロシージャ レベルとモジュール レベルの変数をその型として宣言できます。 たとえば、コンピューター システムに関する情報を記録する構造体を作成できます。 次に例を示します。

```vb
Public Structure systemInfo
    Public cPU As String
    Public memory As Long
    Public purchaseDate As Date
End Structure
```

これで、その型の変数を宣言できるようになりました。 これを次の宣言に示します。

```vb
Dim mySystem, yourSystem As systemInfo
```

> [!NOTE]
> クラスとモジュールで、[Dim ステートメント](../../../language-reference/statements/dim-statement.md)を使用して宣言された構造体は、既定でパブリック アクセスになります。 構造体をプライベートにする場合は、[Private](../../../language-reference/modifiers/private.md) キーワードを使用して宣言してください。

## <a name="access-to-structure-values"></a>構造体の値へのアクセス

構造体変数の要素の値を代入したり取得したりするには、オブジェクトのプロパティの設定と取得に使用するのと同じ構文を使用します。 構造体変数名と要素名の間に、メンバー アクセス演算子 (`.`) を指定します。 次の例は、前に型 `systemInfo` として宣言された変数の要素にアクセスします。

```vb
mySystem.cPU = "486"
Dim tooOld As Boolean
If yourSystem.purchaseDate < #1/1/1992# Then tooOld = True
```

## <a name="assigning-structure-variables"></a>構造体の変数の代入

また、両方が同じ構造体型である場合は、1 つの変数を別の変数に代入することもできます。 これにより、1 つの構造体のすべての要素が、もう一方の対応する要素にコピーされます。 これを次の宣言に示します。

```vb
yourSystem = mySystem
```

構造体要素が `String`、`Object`、配列などの参照型である場合は、データへのポインターがコピーされます。 前の例で、`systemInfo` にオブジェクト変数が含まれているとすると、ポインターが `mySystem` から `yourSystem` にコピーされています。また、1 つの構造体を介してオブジェクトのデータを変更すると、他の構造体を使用してアクセスしたときに有効になります。

## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [基本データ型](elementary-data-types.md)
- [複合データ型](composite-data-types.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [構造体](structures.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
- [方法: 構造体を宣言する](how-to-declare-a-structure.md)
- [構造体とその他のプログラミング要素](structures-and-other-programming-elements.md)
- [構造体とクラス](structures-and-classes.md)
- [Structure ステートメント](../../../language-reference/statements/structure-statement.md)
