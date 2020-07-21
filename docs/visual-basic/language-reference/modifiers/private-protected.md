---
title: Private Protected
ms.date: 05/10/2018
helpviewer_keywords:
- Private Protected keyword [Visual Basic]
- Private Protected keyword [Visual Basic], syntax
ms.openlocfilehash: b7d9f81e41950b92c787e2e50fb94fe3d7c07559
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84362230"
---
# <a name="private-protected-visual-basic"></a>Private Protected (Visual Basic)

キーワード組み合わせ `Private Protected` はメンバー アクセス修飾子です。 `Private Protected` メンバーは、その親クラスのすべてのメンバーと、親クラスから派生した型でアクセスできますが、それらがその親アセンブリにも存在する場合に限られます。

`Private Protected` は、クラスのメンバーに対してのみ指定できます。構造体は継承できないため、構造体のメンバーに `Private Protected` を適用することはできません。

`Private Protected` アクセス修飾子は Visual Basic 15.5 以降でサポートされています。 これを使用するには、次の要素を Visual Basic プロジェクト (\*.vbproj) ファイルに追加します。 システムに Visual Basic 15.5 以降がインストールされている限り、Visual Basic コンパイラの最新バージョンでサポートされているすべての言語機能を利用できます。

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

詳細については、[Visual Basic 言語バージョンの設定](../configure-language-version.md)に関するページを参照してください。

> [!NOTE]
> Visual Studio で、`private protected` に対して F1 ヘルプを選択すると、[private](private.md) または [protected](protected.md) のヘルプが表示されます。 IDE では、複合語ではなくカーソルの下にある 1 つのトークンが選択されます。

## <a name="rules"></a>ルール

- **宣言コンテキスト。** `Private Protected` は、クラス レベルでのみ使用できます。 つまり、`Protected` 要素の宣言コンテキストはクラスにする必要があり、ソース ファイル、名前空間、インターフェイス、モジュール、構造体、またはプロシージャにすることはできません。

## <a name="behavior"></a>動作

- **アクセス レベル。** クラス内のすべてのコードで、その要素にアクセスできます。 基底クラスから派生し、同じアセンブリに含まれるすべてのクラスのコードで、基底クラスのすべての `Private Protected` 要素にアクセスできます。 ただし、基底クラスから派生し、別のアセンブリに含まれるクラスのコードでは、基底クラスの `Private Protected` 要素にアクセスできません。

- **アクセス修飾子。** アクセス レベルを指定するキーワードは、*アクセス修飾子*と呼ばれます。 アクセス修飾子の比較については、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

`Private Protected` 修飾子は、次のコンテキストで使用できます。

- 入れ子になったクラスの [Class ステートメント](../statements/class-statement.md)

- [Const ステートメント](../statements/const-statement.md)

- [Declare ステートメント](../statements/declare-statement.md)

- クラスに入れ子にされたデリゲートの [Delegate ステートメント](../statements/delegate-statement.md)

- [Dim ステートメント](../statements/dim-statement.md)

- クラスに入れ子にされた列挙型の [Enum ステートメント](../statements/enum-statement.md)

- [Event ステートメント](../statements/event-statement.md)

- [Function ステートメント](../statements/function-statement.md)

- クラスに入れ子にされたインターフェイスの [Interface ステートメント](../statements/interface-statement.md)

- [Property ステートメント](../statements/property-statement.md)

- クラスに入れ子にされた構造体の[Structure ステートメント](../statements/structure-statement.md)

- [Sub ステートメント](../statements/sub-statement.md)

## <a name="see-also"></a>関連項目

- [Public](public.md)
- [Protected](protected.md)
- [Friend](friend.md)
- [Private](private.md)
- [Protected Friend](./protected-friend.md)
- [Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)
- [手順](../../programming-guide/language-features/procedures/index.md)
- [構造体](../../programming-guide/language-features/data-types/structures.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
