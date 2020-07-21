---
title: Overrides
ms.date: 07/20/2015
f1_keywords:
- Overrides
- vb.Overrides
helpviewer_keywords:
- properties [Visual Basic], redefining
- procedures [Visual Basic], overriding
- procedures [Visual Basic], redefining
- overriding
- Overrides keyword [Visual Basic]
- overriding, Overrides keyword
- properties [Visual Basic], overriding
ms.assetid: 9f5e6144-ce10-465e-842b-1a8f8760af90
ms.openlocfilehash: 657f838b2959a5b6a7cef5ff18295a4ada709e9a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392029"
---
# <a name="overrides-visual-basic"></a>Overrides (Visual Basic)

プロパティまたはプロシージャが基本クラスから継承された同じ名前のプロパティまたはプロシージャをオーバーライドすることを示します。

## <a name="rules"></a>ルール

- **宣言コンテキスト。** `Overrides` は、プロパティまたはプロシージャの宣言ステートメントでのみ使用できます。

- **結合された修飾子。** 同じ宣言内で `Overrides` を `Shadows` または `Shared` と共に指定することはできません。 オーバーライドする要素は暗黙的にオーバーライド可能であるため、`Overridable` と `Overrides` を結合することはできません。

- **シグネチャの一致。** この宣言のシグネチャは、オーバーライドされるプロパティまたはプロシージャの*シグネチャ*と完全に一致する必要があります。 つまり、パラメーター リストには、同じ数のパラメーターを、同じ順序、同じデータ型で指定する必要があります。

  オーバーライドする宣言は、シグネチャに加え、次の点でも完全に一致している必要があります。

  - アクセス レベル

  - 戻り値の型 (戻り値がある場合)

- **ジェネリック シグネチャ。** ジェネリック プロシージャでは、シグネチャに型パラメーターの数が含まれます。 したがって、オーバーライドする宣言は、その点でも基底クラスのバージョンに一致している必要があります。

- **その他の一致。** この宣言は、基底クラスのバージョンのシグネチャに一致していることに加え、次の点でも基底クラスと一致している必要があります。

  - アクセス レベル修飾子 ([Public](public.md) など)

  - 各パラメーターの引き渡し方法 ([ByVal](byval.md) または [ByRef](byref.md))

  - ジェネリック プロシージャの型パラメーターごとの制約リスト

- **シャドウとオーバーライド。** シャドウとオーバーライドは、どちらも継承された要素を再定義しますが、その方法は大きく異なります。 詳細については、「[Visual Basic におけるシャドウ](../../programming-guide/language-features/declared-elements/shadowing.md)」を参照してください。

`Overrides` を使用する場合は、ライブラリ API と C# が連携しやすくなるように、コンパイラが暗黙的に `Overloads` を追加します。

`Overrides` 修飾子は、次のコンテキストで使用できます。

- [Function ステートメント](../statements/function-statement.md)

- [Property ステートメント](../statements/property-statement.md)

- [Sub ステートメント](../statements/sub-statement.md)

## <a name="see-also"></a>関連項目

- [MustOverride](mustoverride.md)
- [NotOverridable](notoverridable.md)
- [Overridable](overridable.md)
- [キーワード](../keywords/index.md)
- [Visual Basic におけるシャドウ](../../programming-guide/language-features/declared-elements/shadowing.md)
- [Generic Types in Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [型リスト](../statements/type-list.md)
