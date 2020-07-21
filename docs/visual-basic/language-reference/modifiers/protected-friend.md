---
title: Protected Friend
ms.date: 05/10/2018
helpviewer_keywords:
- Protected Friend keyword [Visual Basic]
- Protected Friend keyword [Visual Basic], syntax
ms.openlocfilehash: 202d4f4a3a05a64ab1d74621268f28f6b55e8952
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404837"
---
# <a name="protected-friend-visual-basic"></a>Protected Friend (Visual Basic)

キーワード組み合わせ `Protected Friend` はメンバー アクセス修飾子です。 宣言された要素に対して、[Friend](friend.md) アクセスと [Protected](protected.md) アクセスの両方が許可されるため、同じアセンブリ内の任意の場所から、それらの独自のクラスから、および派生クラスから、それらにアクセスできます。 `Protected Friend` は、クラスのメンバーに対してのみ指定できます。構造体は継承できないため、構造体のメンバーに `Protected Friend` を適用することはできません。

> [!NOTE]
> Visual Studio で、`protected friend` に対して F1 ヘルプを選択すると、[protected](protected.md) または [friend](friend.md) のヘルプが表示されます。 IDE では、複合語ではなくカーソルの下にある 1 つのトークンが選択されます。

## <a name="rules"></a>ルール

**宣言コンテキスト。** `Protected Friend` は、クラス レベルでのみ使用できます。 つまり、`Protected` 要素の宣言コンテキストはクラスにする必要があり、ソース ファイル、名前空間、インターフェイス、モジュール、構造体、またはプロシージャにすることはできません。

## <a name="see-also"></a>関連項目

- [Public](public.md)
- [Protected](protected.md)
- [Friend](friend.md)
- [Private](private.md)
- [Private Protected](./private-protected.md)
- [Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)
- [手順](../../programming-guide/language-features/procedures/index.md)
- [構造体](../../programming-guide/language-features/data-types/structures.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
