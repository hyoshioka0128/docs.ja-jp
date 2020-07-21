---
title: オブジェクト変数の代入
ms.date: 07/20/2015
helpviewer_keywords:
- Nothing keyword [Visual Basic], object variable assignment
- object variables [Visual Basic], initializing
- variables [Visual Basic], initializing
- objects [Visual Basic], current instance
- object variables [Visual Basic], assigning
- variables [Visual Basic], object variables
- current instance [Visual Basic], defined
- variables [Visual Basic], assigning
- assignment statements [Visual Basic], object variable assignment
- Me keyword [Visual Basic], as object variable
ms.assetid: 3706811d-fd40-44fe-8727-d692e8e55d6d
ms.openlocfilehash: 9ae1a307e8c886166d516140b7f100a411cedcfa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410375"
---
# <a name="object-variable-assignment-visual-basic"></a>オブジェクト変数への代入 (Visual Basic)

オブジェクトにオブジェクト変数を代入するには、通常の代入ステートメントを使用します。 次の例で示すように、オブジェクト式または [Nothing](../../../language-reference/nothing.md) キーワードを代入することができます。

```vb
Dim thisObject As Object
' The following statement assigns an object reference.
thisObject = Form1
' The following statement discontinues association with any object.
thisObject = Nothing
```

`Nothing` は、現在変数に代入されているオブジェクトがないことを意味します。

## <a name="initialization"></a>初期化

コードの実行が開始されると、オブジェクト変数は、`Nothing` に初期化されます。 宣言に初期化を含むものは、宣言ステートメントの実行時に、指定された値に再初期化されます。

宣言に初期化を含めるには、[New](../../../language-reference/operators/new-operator.md) キーワードを使用します。 次の宣言ステートメントは、オブジェクト変数 `testUri` と `ver` を宣言し、それらに特定のオブジェクトを代入します。 それぞれは、適切なクラスのオーバーロードされたコンストラクターのいずれかを使用して、オブジェクトを初期化します。

```vb
Dim testUri As New System.Uri("https://www.microsoft.com")
Dim ver As New System.Version(6, 1, 0)
```

## <a name="disassociation"></a>関連付けの解除

オブジェクト変数を `Nothing` に設定すると、変数と特定のオブジェクトの関連付けは解除されます。 これにより、変数の変更によってオブジェクトが誤って変更されることがなくなります。 また、次の例で示すように、オブジェクト変数が有効なオブジェクトを指しているかどうかをテストすることもできます。

```vb
If otherObject IsNot Nothing Then
    ' otherObject refers to a valid object, so your code can use it.
End If
```

変数が参照するオブジェクトが別のアプリケーション内にある場合、このテストでは、そのアプリケーションが終了したか、またはオブジェクトを無効にしただけであるかを判断することはできません。

値が `Nothing` に設定されたオブジェクト変数は、"*null 参照*" とも呼ばれます。

## <a name="current-instance"></a>現在のインスタンス

オブジェクトの "*現在のインスタンス*" は、コードで現在実行されているインスタンスです。 すべてのコードはプロシージャ内で実行されるため、現在のインスタンスは、プロシージャを呼び出したインスタンスです。

`Me` キーワードは、現在のインスタンスを参照するオブジェクト変数として機能します。 プロシージャが [Shared](../../../language-reference/modifiers/shared.md) ではない場合、`Me` キーワードを使用して、現在のインスタンスへのポインターを取得できます。 Shared プロシージャを、クラスの特定のインスタンスに関連付けることはできません。

`Me` は、現在のインスタンスを別のモジュールのプロシージャに渡す場合に使用すると特に有用です。 たとえば、複数の XML ドキュメントがあり、これらのすべてに何らかの標準テキストを追加したいとします。 次の例は、このためのプロシージャを定義します。

```vb
Sub addStandardText(XmlDoc As System.Xml.XmlDocument)
    XmlDoc.CreateTextNode("This text goes into every XML document.")
End Sub
```

すべての XML ドキュメント オブジェクトは、このプロシージャを呼び出して、その現在のインスタンスを引数として渡すことができます。 次に例を示します。

```vb
addStandardText(Me)
```

## <a name="see-also"></a>関連項目

- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の宣言](object-variable-declaration.md)
- [オブジェクト変数の値](object-variable-values.md)
- [方法: Visual Basic でオブジェクト変数を宣言してオブジェクトを代入する](how-to-declare-an-object-variable-and-assign-an-object-to-it.md)
- [方法: オブジェクト変数がインスタンスを参照しないようにする](how-to-make-an-object-variable-not-refer-to-any-instance.md)
- [Me、My、MyBase、および MyClass](../../program-structure/me-my-mybase-and-myclass.md)
