---
title: プロシージャのオーバーロード
ms.date: 07/20/2015
helpviewer_keywords:
- signatures
- Overloads keyword [Visual Basic]
- hiding by signature
- Visual Basic code, procedures
- procedures [Visual Basic], signatures for
- procedures [Visual Basic], overloading
- procedures [Visual Basic], multiple versions
- parameters [Visual Basic], lists
- signatures [Visual Basic], procedure
- parameter lists [Visual Basic]
- Visual Basic code, parameter lists
- Shadows keyword [Visual Basic]
- procedure overloading
- procedures [Visual Basic], parameter lists
ms.assetid: fbc7fb18-e3b2-48b6-b554-64c00ed09d2a
ms.openlocfilehash: f8accc74fbdd9b1d8cf9bc3d8f6ddd26f73452b8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363877"
---
# <a name="procedure-overloading-visual-basic"></a>プロシージャのオーバーロード (Visual Basic)

プロシージャの "*オーバーロード*" は、同じ名前と異なるパラメーター リストを使用して、複数のバージョンでプロシージャを定義することを意味します。 オーバーロードの目的は、名前で区別する必要なく、プロシージャの密接に関連する複数のバージョンを定義することです。 これを行うには、異なるパラメーター リストを使用します。

## <a name="overloading-rules"></a>オーバーロードのルール

プロシージャをオーバーロードするときは、次のルールが適用されます。

- **同じ名前**: 各オーバーロードされたバージョンでは、同じプロシージャ名を使用する必要があります。

- **異なるシグネチャ**: 各オーバーロードされたバージョンは、次の項目の少なくとも 1 つが、他のすべてのオーバーロードされたバージョンと異なる必要があります。

  - パラメーターの数

  - パラメーターの順序

  - パラメーターのデータ型

  - 型パラメーターの数 (ジェネリック プロシージャの場合)

  - 戻り値の型 (変換演算子の場合のみ)

  プロシージャ名と組み合わされた上記の項目を総称して、プロシージャの "*シグネチャ*" と呼びます。 オーバーロードされたプロシージャを呼び出すと、コンパイラはシグネチャを使用して、その呼び出しが定義と正しく一致することを確認します。

- **シグネチャに含まれない項目**: シグネチャを変えずにプロシージャをオーバーロードすることはできません。 具体的には、次の 1 つ以上の項目が異なるだけでは、プロシージャをオーバーロードすることはできません。

  - プロシージャ修飾子キーワード (`Public`、`Shared`、`Static` など)

  - パラメーター名または型パラメーター名

  - 型パラメーターの制約 (ジェネリック プロシージャの場合)

  - パラメーター修飾子キーワード (`ByRef` や `Optional` など)

  - 値を返すかどうか

  - 戻り値のデータ型 (変換演算子を除く)

  上記の一覧の項目は、シグネチャには含まれません。 これらを使用してオーバーロードされたバージョンを区別することはできませんが、シグネチャによって適切に区別されているオーバーロードされたバージョン間でこれらを変えることは可能です。

- **遅延バインディングされた引数**: 遅延バインディングされたオブジェクト変数をオーバーロードされたバージョンに渡す場合は、適切なパラメーターを <xref:System.Object> として宣言する必要があります。

## <a name="multiple-versions-of-a-procedure"></a>プロシージャの複数のバージョン

顧客の残高に対してトランザクションを転記する `Sub` プロシージャを作成し、名前または口座番号で顧客を参照できるようにするとします。 これに対応するために、次の例のように、2 つの異なる `Sub` プロシージャを定義できます。

[!code-vb[VbVbcnProcedures#73](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#73)]

### <a name="overloaded-versions"></a>オーバーロードされたバージョン

別の方法として、単一のプロシージャ名をオーバーロードします。 次のように、[Overloads](../../../language-reference/modifiers/overloads.md) キーワードを使用して、パラメーター リストごとにプロシージャのバージョンを定義できます。

[!code-vb[VbVbcnProcedures#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#72)]

#### <a name="additional-overloads"></a>追加のオーバーロード

取引金額を `Decimal` または `Single` で受け入れることも必要な場合は、`post` をさらにオーバーロードしてこのバリエーションに対応できます。 前の例の各オーバーロードに対してこれを行う場合、すべて同じ名前で 4 つの異なるシグネチャを持つ 4 つの `Sub` プロシージャを作成します。

## <a name="advantages-of-overloading"></a>オーバーロードの利点

プロシージャをオーバーロードする利点は、呼び出しの柔軟性にあります。 前の例で宣言された `post` プロシージャを使用する場合、呼び出し元のコードで `String` または `Integer` として顧客 ID を取得し、どちらの場合も同じプロシージャを呼び出すことができます。 次に例を示します。

[!code-vb[VbVbcnProcedures#56](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#56)]

[!code-vb[VbVbcnProcedures#57](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#57)]

## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [方法: プロシージャの複数のバージョンを定義する](./how-to-define-multiple-versions-of-a-procedure.md)
- [方法: オーバーロードされたプロシージャを呼び出す](./how-to-call-an-overloaded-procedure.md)
- [方法: 省略可能なパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [方法: 不特定数のパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)
- [オーバーロードの解決](./overload-resolution.md)
- [Overloads](../../../language-reference/modifiers/overloads.md)
- [Generic Types in Visual Basic](../data-types/generic-types.md)
