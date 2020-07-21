---
title: インポート '<qualifiedelementname>' で指定された名前空間または型が、パブリック メンバーを含んでいないか、または見つかりません。
ms.date: 07/20/2015
f1_keywords:
- bc40056
- vbc40056
helpviewer_keywords:
- BC40056
ms.assetid: b59f5754-444f-4378-9272-9678b437e84a
ms.openlocfilehash: 8675d9c3b202200c89e12e7a5f51a19d9e3e0e64
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409466"
---
# <a name="namespace-or-type-specified-in-the-imports-qualifiedelementname-doesnt-contain-any-public-member-or-cannot-be-found"></a>インポート '\<qualifiedelementname>' で指定された名前空間または型が、パブリック メンバーを含んでいないか、または見つかりません。

インポート '\<qualifiedelementname>' で指定された名前空間または型が、パブリック メンバーを含んでいないか、または見つかりません。 名前空間または型が定義されており、少なくとも 1 つのパブリック メンバーが含まれていることを確認してください。 別名の名前に他の別名が含まれていないことを確認してください。

`Imports` ステートメントは、見つからないか、`Public` メンバーを定義しないコンテナー要素を指定しています。

*コンテナー要素*は、名前空間、クラス、構造体、モジュール、インターフェイス、または列挙型にすることができます。 コンテナー要素には、変数、プロシージャ、その他のコンテナー要素などのメンバーが含まれています。

インポートの目的は、コードによって名前空間または型のメンバーに、それらを修飾しなくてもアクセスできるようにすることです。 また、プロジェクトで名前空間や型への参照を追加する必要がある場合もあります。 詳細については、「[宣言された要素の参照](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)」の "コンテナー要素のインポート" に関するセクションを参照してください。

コンパイラは、指定したコンテナー要素が見つからない場合、それを使用する参照を解決できません。 要素が見つかったが、要素が `Public` のメンバーを公開していない場合、参照を正常に実行できません。 どちらの場合も、要素をインポートしても意味がありません。

コンテナー要素をインポートし、それにインポートの別名を割り当てた場合は、その別名を使用して別の要素をインポートできないことに注意してください。 次のコードはコンパイラ エラーになります。

```vb
Imports winfrm = System.Windows.Forms

' The following statement is INVALID  because it reuses an import alias.

Imports behave = winfrm.Design.Behavior`
```

**エラー ID:** BC40056

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. コンテナー要素がプロジェクトからアクセス可能であることを確認します。

2. コンテナー要素の指定に、別のインポートの別名が含まれていないことを確認します。

3. コンテナー要素が少なくとも 1 つの `Public` メンバーを公開していることを確認します。

## <a name="see-also"></a>関連項目

- [Imports ステートメント (.NET 名前空間および型)](../statements/imports-statement-net-namespace-and-type.md)
- [Namespace ステートメント](../statements/namespace-statement.md)
- [Public](../modifiers/public.md)
- [Visual Basic における名前空間](../../programming-guide/program-structure/namespaces.md)
- [宣言された要素の参照](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
