---
title: '方法: オブジェクトのメンバーにアクセスする'
ms.date: 07/20/2015
helpviewer_keywords:
- members [Visual Basic], accessing
- object variables [Visual Basic], accessing members
ms.assetid: a0072514-6a79-4dd6-8d03-ca8c13e61ddc
ms.openlocfilehash: 2826a3c98b9f19b08cc943d0f67cdd34ac90f526
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410543"
---
# <a name="how-to-access-members-of-an-object-visual-basic"></a>方法: オブジェクトのメンバーにアクセスする (Visual Basic)

オブジェクトを参照しているオブジェクト変数がある場合、そのオブジェクトのメンバー (メソッド、プロパティ、フィールド、イベントなど) を使いたいことがよくあります。 たとえば、新しい <xref:System.Windows.Forms.Form> オブジェクトを作成した後、その <xref:System.Windows.Forms.Control.Text%2A> プロパティを設定したり、その <xref:System.Windows.Forms.Control.Focus%2A> メソッドを呼び出したりする場合です。

## <a name="accessing-members"></a>メンバーへのアクセス

オブジェクトのメンバーには、それを参照している変数を使用してアクセスします。

#### <a name="to-access-members-of-an-object"></a>オブジェクトのメンバーにアクセスするには

- オブジェクト変数名とメンバー名の間に、メンバー アクセス演算子 (`.`) を使用します。

    ```vb
    currentText = newForm.Text
    ```

    メンバーが [Shared](../../../language-reference/modifiers/shared.md) である場合は、そのメンバーにアクセスするために変数は必要ありません。

## <a name="accessing-members-of-an-object-of-known-type"></a>既知の型のオブジェクトのメンバーへのアクセス

コンパイル時にオブジェクトの型がわかっている場合は、それを参照している変数に対して "*事前バインディング*" を使用できます。

#### <a name="to-access-members-of-an-object-for-which-you-know-the-type-at-compile-time"></a>コンパイル時に型がわかっているオブジェクトのメンバーにアクセスするには

1. 変数に割り当てるオブジェクトの型として、オブジェクト変数を宣言します。

    ```vb
    Dim extraForm As System.Windows.Forms.Form
    ```

    `Option Strict On` を使用すると、<xref:System.Windows.Forms.Form> オブジェクト (または、<xref:System.Windows.Forms.Form> から派生した型のオブジェクト) のみを、`extraForm` に割り当てることができます。 <xref:System.Windows.Forms.Form> への `CType` 拡大変換を使用してクラスまたは構造体を定義した場合は、そのクラスまたは構造体を `extraForm` に割り当てることもできます。

2. オブジェクト変数名とメンバー名の間に、メンバー アクセス演算子 (`.`) を使用します。

    ```vb
    extraForm.Show()
    ```

    `Option Strict` の設定に関係なく、<xref:System.Windows.Forms.Form> クラスに固有のすべてのメソッドとプロパティにアクセスすることができます。

## <a name="accessing-members-of-an-object-of-unknown-type"></a>型が不明なオブジェクトのメンバーへのアクセス

コンパイル時にオブジェクトの型がわからない場合は、それを参照している変数に対して "*遅延バインディング*" を使用する必要があります。

#### <a name="to-access-members-of-an-object-for-which-you-do-not-know-the-type-at-compile-time"></a>コンパイル時に型がわからないオブジェクトのメンバーにアクセスするには

1. オブジェクト変数を [Object データ型](../../../language-reference/data-types/object-data-type.md)として宣言します。 (変数を `Object` として宣言することは、<xref:System.Object?displayProperty=nameWithType> として宣言することと同じです。)

    ```vb
    Dim someControl As Object
    ```

    `Option Strict On` を使用すると、<xref:System.Object> クラスで定義されているメンバーにのみアクセスすることができます。

2. オブジェクト変数名とメンバー名の間に、メンバー アクセス演算子 (`.`) を使用します。

    ```vb
    someControl.GetType()
    ```

    オブジェクト変数に割り当てる任意のオブジェクトのメンバーにアクセスできるようにするには、`Option Strict Off` を設定する必要があります。 このようにすると、変数に割り当てたオブジェクトによって特定のメンバーが公開されていることを、コンパイラでは保証できません。 アクセスしようとしたメンバーがオブジェクトによって公開されていない場合、<xref:System.MemberAccessException> 例外が発生します。

## <a name="see-also"></a>関連項目

- <xref:System.Object>
- <xref:System.Windows.Forms.Form>
- <xref:System.MemberAccessException>
- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の宣言](object-variable-declaration.md)
- [Object 型](../../../language-reference/data-types/object-data-type.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
