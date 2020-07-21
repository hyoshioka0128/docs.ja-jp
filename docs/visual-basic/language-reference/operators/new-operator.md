---
title: new 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.new
- vb.NewConstraint
helpviewer_keywords:
- constraints, Visual Basic generic types
- generics [Visual Basic], constraints
- constraints, New keyword [Visual Basic]
- New constraint
- New keyword [Visual Basic]
ms.assetid: d7d566d7-fe0e-4336-91f7-641a542de4d0
ms.openlocfilehash: 27b5b4516ef729045036c36fedc24b6c576a4f61
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74348314"
---
# <a name="new-operator-visual-basic"></a>New 演算子 (Visual Basic)

新しいオブジェクト インスタンスを作成するための `New` 句の導入、型パラメーターでのコンストラクター制約の指定、またはクラス コンストラクターとして `Sub` プロシージャの指定を行います。

## <a name="remarks"></a>Remarks

宣言または代入ステートメントで、`New` 句によって、インスタンスの作成元として使用できる定義済みのクラスを指定する必要があります。 つまり、このクラスによって、呼び出し元のコードがアクセスできる 1 つ以上のコンストラクターが公開されなければなりません。

`New` 句は、宣言ステートメントまたは代入ステートメントで使用できます。 このステートメントが実行されると、指定したクラスの適切なコンストラクターが呼び出され、指定した引数が渡されます。 これを示す例を次に紹介します。2 つのコンストラクターがある `Customer` クラスのインスタンスを作成し、コンストラクターの 1 つはパラメーターを受け取らず、もう 1 つは文字列パラメーターを受け取ります。

[!code-vb[VbVbalrKeywords#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class6.vb#11)]

配列はクラスであるため、次の例に示すように、`New` によって新しい配列インスタンスを作成できます。

[!code-vb[VbVbalrKeywords#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/Class6.vb#12)]

新しいインスタンスを作成するためのメモリが不足している場合、共通言語ランタイム (CLR) は <xref:System.OutOfMemoryException> エラーをスローします。

> [!NOTE]
> `New` キーワードを型パラメーター リストで使用して、指定した型が、アクセス可能なパラメーターなしのコンストラクターを公開する必要があること指定することもできます。 型パラメーターと制約の詳細については、「[型リスト](../statements/type-list.md)」を参照してください。

クラスのコンストラクター プロシージャを作成するには、`Sub` プロシージャの名前を `New` キーワードに設定します。 詳細については、以下をご覧ください: [オブジェクトの有効期間: オブジェクトの作成と破棄](../../programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)

キーワード `New` は次のコンテキストで使用できます。

- [Dim ステートメント](../statements/dim-statement.md)
- [Of](../statements/of-clause.md)
- [Sub ステートメント](../statements/sub-statement.md)

## <a name="see-also"></a>関連項目

- <xref:System.OutOfMemoryException>
- [キーワード](../keywords/index.md)
- [型リスト](../statements/type-list.md)
- [Generic Types in Visual Basic](../../programming-guide/language-features/data-types/generic-types.md)
- [オブジェクトの有効期間: オブジェクトの作成と破棄](../../programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)
