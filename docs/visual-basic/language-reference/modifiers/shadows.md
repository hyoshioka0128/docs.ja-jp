---
title: Overloads
ms.date: 07/20/2015
f1_keywords:
- vb.Shadows
- shadows
helpviewer_keywords:
- shadowing
- duplicate names [Visual Basic]
- scope [Visual Basic], shadowing
- Shadows keyword [Visual Basic]
- names [Visual Basic], shadowing
ms.assetid: 6bf687cd-0544-4797-b51b-911125ec57c6
ms.openlocfilehash: 7aed6bec21bd484cca019b061bd5915de13a9eb8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402708"
---
# <a name="shadows-visual-basic"></a>Shadows (Visual Basic)

宣言されたプログラミング要素が、基底クラスにある、同じ名前を持つ要素、またはオーバーロードされる要素のセットを宣言し直して非表示にすることを示します。

## <a name="remarks"></a>Remarks

シャドウ (*名前による非表示*とも呼ばれます) の主な目的は、クラス メンバーの定義を保持することです。 基底クラスには、既に定義されているものと同じ名前の要素を作成する変更が含まれる場合があります。 この場合、`Shadows` 修飾子は、クラスによる参照が、新しい基底クラス要素ではなく定義したメンバーに強制的に解決されるようにします。

シャドウとオーバーライドは、どちらも継承された要素を再定義しますが、その方法は大きく異なります。 詳細については、「[Visual Basic におけるシャドウ](../../programming-guide/language-features/declared-elements/shadowing.md)」を参照してください。

## <a name="rules"></a>ルール

- **宣言コンテキスト。** `Shadows` は、クラス レベルでのみ使用できます。 つまり、`Shadows` 要素の宣言コンテキストはクラスにする必要があり、ソース ファイル、名前空間、インターフェイス、モジュール、構造体、またはプロシージャにすることはできません。

  1 つの宣言ステートメントでは、シャドウ要素を 1 つだけ宣言できます。

- **結合された修飾子。** 同じ宣言内で `Shadows` を `Overloads`、`Overrides`、または `Static` と共に指定することはできません。

- **要素型。** 宣言された要素は、他の任意の種類の要素でシャドウできます。 別のプロパティまたはプロシージャを使用してプロパティまたはプロシージャをシャドウする場合、パラメーターと戻り値の型が基底クラスのプロパティまたはプロシージャ内のパラメーターと一致する必要はありません。

- **アクセス。** 基底クラス内のシャドウされた要素は、通常、それをシャドウする派生クラス内からは使用できません。 ただし、次の考慮事項が適用されます。

  - シャドウ要素が、それを参照するコードからアクセスできない場合、参照はシャドウされた要素に解決されます。 たとえば、`Private` 要素が基底クラスの要素をシャドウすると、`Private` 要素へのアクセス許可を持たないコードが、代わりに基底クラスの要素にアクセスします。

  - 要素をシャドウする場合でも、基底クラスの型で宣言されたオブジェクトを使用して、シャドウされた要素にアクセスできます。 また、`MyBase` を使用してアクセスすることもできます。

`Shadows` 修飾子は、次のコンテキストで使用できます。

- [Class ステートメント](../statements/class-statement.md)

- [Const ステートメント](../statements/const-statement.md)

- [Declare ステートメント](../statements/declare-statement.md)

- [Delegate ステートメント](../statements/delegate-statement.md)

- [Dim ステートメント](../statements/dim-statement.md)

- [Enum ステートメント](../statements/enum-statement.md)

- [Event ステートメント](../statements/event-statement.md)

- [Function ステートメント](../statements/function-statement.md)

- [Interface ステートメント](../statements/interface-statement.md)

- [Property ステートメント](../statements/property-statement.md)

- [Structure ステートメント](../statements/structure-statement.md)

- [Sub ステートメント](../statements/sub-statement.md)

## <a name="see-also"></a>関連項目

- [Shared](shared.md)
- [Static](static.md)
- [Private](private.md)
- [Me、My、MyBase、および MyClass](../../programming-guide/program-structure/me-my-mybase-and-myclass.md)
- [継承の基本](../../programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [MustOverride](mustoverride.md)
- [NotOverridable](notoverridable.md)
- [Overloads](overloads.md)
- [Overridable](overridable.md)
- [Overrides](overrides.md)
- [Visual Basic におけるシャドウ](../../programming-guide/language-features/declared-elements/shadowing.md)
