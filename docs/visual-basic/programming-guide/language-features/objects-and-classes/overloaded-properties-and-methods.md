---
title: オーバーロードされたプロパティとメソッド
ms.date: 07/20/2015
helpviewer_keywords:
- properties [Visual Basic], overloading
- methods [Visual Basic], overloading
- shadowing
- names [Visual Basic], multiple procedures with same
- procedures [Visual Basic], multiples with same name
- classes [Visual Basic], properties
- classes [Visual Basic], methods
- method overloading
- Overloads keyword [Visual Basic], overloaded members
ms.assetid: b686fb97-e7d7-4001-afaa-6650cba08f0d
ms.openlocfilehash: 1672f12773ece012c580253b6dafbf9d0ac8f07c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84389153"
---
# <a name="overloaded-properties-and-methods-visual-basic"></a>オーバーロードされたプロパティとメソッド (Visual Basic)

オーバーロードとは、名前が同じで引数の型が異なる複数のプロシージャ、インスタンスのコンストラクター、またはプロパティをクラスに作成することです。

## <a name="overloading-usage"></a>オーバーロードの使用法

オーバーロードは、さまざまなデータ型を操作するプロシージャに同じ名前を使用するようにオブジェクト モデルで指示された場合に特に便利です。 たとえば、各種のデータ型を表示できるクラスには、次のような `Display` プロシージャがある場合があります。

[!code-vb[VbVbalrOOP#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#64)]

オーバーロードを使用しない場合は、実行する処理は同じでも、次に示すようにプロシージャごとに個別の名前を作成する必要があります。

[!code-vb[VbVbalrOOP#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#65)]

オーバーロードを使用すると、使用可能なデータ型を選択できるため、プロパティやメソッドを簡単に使用できるようになります。 たとえば、前に説明したオーバーロードされた `Display` メソッドは、次のいずれかのコード行を使用して呼び出すことができます。

[!code-vb[VbVbalrOOP#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#66)]

実行時に、Visual Basic は、指定されたパラメーターのデータ型に基づいて正しいプロシージャを呼び出します。

## <a name="overloading-rules"></a>オーバーロードのルール

 オーバーロードされたメンバーをクラスに作成するには、同じ名前を持つ 2 つ以上のプロパティまたはメソッドを追加します。 オーバーロードされた派生メンバーを除き、オーバーロードされた各メンバーは異なるパラメーター リストを持つ必要があります。また、プロパティまたはプロシージャをオーバーロードするときに、区別するための特性として次の項目を使用することはできません。

- メンバーまたはメンバーのパラメーターに適用される、`ByVal` や `ByRef` などの修飾子。

- パラメーターの名前

- プロシージャの戻り値の型

`Overloads` キーワードはオーバーロード時には省略可能ですが、オーバーロードされたメンバーが `Overloads` キーワードを使用している場合は、同じ名前の他のすべてのオーバーロードされたメンバーにもこのキーワードを指定する必要があります。

派生クラスでは、継承されたメンバーを同じパラメーターとパラメーターの型を持つメンバーでオーバーロードすることができます。これは、*名前とシグネチャによるシャドウ*と呼ばれる処理です。 名前とシグネチャによるシャドウを行うときに `Overloads` キーワードを使用すると、基底クラスの実装ではなく、派生クラスのメンバーの実装が使用され、そのメンバーの他のすべてのオーバーロードが派生クラスのインスタンスで使用できるようになります。

同じパラメーターとパラメーターの型を持つメンバーで継承されたメンバーをオーバーロードするときに `Overloads` キーワードを省略した場合、そのオーバーロードは*名前によるシャドウ*と呼ばれます。 名前によるシャドウでは、メンバーの継承された実装が置き換えられます。これにより、派生クラスとその子孫のインスタンスで他のすべてのオーバーロードが使用できなくなります。

`Overloads` と `Shadows` の両方の修飾子を同じプロパティまたはメソッドで使用することはできません。

### <a name="example"></a>例

次の例では、`String` または `Decimal` で表現されたドル額を受け取り、売上税を含む文字列を返すオーバーロードされたメソッドを作成しています。

#### <a name="to-use-this-example-to-create-an-overloaded-method"></a>この例を使用して、オーバーロードされたメソッドを作成するには

1. 新しいプロジェクトを開いて、`TaxClass` という名前のクラスを追加します。

2. `TaxClass` クラスに次のコードを追加します。

    [!code-vb[VbVbalrOOP#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#67)]

3. 次のプロシージャをフォームに追加します。

    [!code-vb[VbVbalrOOP#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#68)]

4. フォームにボタンを追加し、ボタンの `Button1_Click` イベントから `ShowTax` プロシージャが呼び出されるようにします。

5. プロジェクトを実行し、フォームのボタンをクリックして、オーバーロードされた `ShowTax` プロシージャをテストします。

実行時に、コンパイラは、使用されているパラメーターに一致するオーバーロードされた適切な関数を選択します。 このボタンをクリックすると、最初に、文字列である `Price` パラメーターを使用して、オーバーロードされたメソッドが呼び出され、"Price is a String. Tax is $5.12" というメッセージが表示されます。 2 回目は、`Decimal` 値を使用して `TaxAmount` が呼び出され、"Price is a Decimal. Tax is $5.12" というメッセージが表示されます。

## <a name="see-also"></a>関連項目

- [クラスとオブジェクト](index.md)
- [Visual Basic におけるシャドウ](../declared-elements/shadowing.md)
- [Sub ステートメント](../../../language-reference/statements/sub-statement.md)
- [継承の基本](inheritance-basics.md)
- [Shadows](../../../language-reference/modifiers/shadows.md)
- [ByVal](../../../language-reference/modifiers/byval.md)
- [ByRef](../../../language-reference/modifiers/byref.md)
- [Overloads](../../../language-reference/modifiers/overloads.md)
- [Shadows](../../../language-reference/modifiers/shadows.md)
