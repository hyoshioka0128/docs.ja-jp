---
title: 匿名型の定義
ms.date: 07/20/2015
helpviewer_keywords:
- anonymous types [Visual Basic], type definition
ms.assetid: 7a8a0ddc-55ba-4d67-869e-87a84d938bac
ms.openlocfilehash: 952eb295cc71eab5d0ad6e18f2b697a9b701b434
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404902"
---
# <a name="anonymous-type-definition-visual-basic"></a>匿名型の定義 (Visual Basic)

匿名型のインスタンスの宣言に応答して、コンパイラでは、型に対して指定されたプロパティを含む新しいクラス定義を作成します。

## <a name="compiler-generated-code"></a>コンパイラで生成されたコード

次の `product` の定義では、コンパイラで、`Name`、`Price`、および `OnHand` プロパティを含む新しいクラス定義を作成します。

[!code-vb[VbVbalrAnonymousTypes#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#25)]

クラス定義には、次のようなプロパティ定義が含まれています。 キー プロパティに `Set` メソッドがないことに注目してください。 キー プロパティの値は読み取り専用です。

```vb
Public Class $Anonymous1
    Private _name As String
    Private _price As Double
    Private _onHand As Integer
     Public ReadOnly Property Name() As String
        Get
            Return _name
        End Get
    End Property

    Public ReadOnly Property Price() As Double
        Get
            Return _price
        End Get
    End Property

    Public Property OnHand() As Integer
        Get
            Return _onHand
        End Get
        Set(ByVal Value As Integer)
            _onHand = Value
        End Set
    End Property

End Class
```

また、匿名型の定義には、パラメーターなしのコンストラクターが含まれています。 パラメーターを必要とするコンストラクターは許可されません。

匿名型の定義に少なくとも 1 つのキー プロパティが含まれている場合は、<xref:System.Object> から継承された 3 つのメンバー (<xref:System.Object.Equals%2A>、<xref:System.Object.GetHashCode%2A>、<xref:System.Object.ToString%2A>) がこの型定義でオーバーライドされます。 キー プロパティが宣言されていない場合は、<xref:System.Object.ToString%2A> のみがオーバーライドされます。 オーバーライドでは次の機能が提供されます。

- 2 つの匿名型のインスタンスが同じインスタンスである場合、または次の条件を満たしている場合、`Equals` で `True` が返されます。

  - それらのプロパティの数が同じである。

  - プロパティが同じ順序で宣言され、名前と推論された型が同じである。 名前の比較では大文字と小文字は区別されません。

  - 少なくとも 1 つのプロパティがキー プロパティであり、`Key` キーワードが同じプロパティに適用されている。

  - キー プロパティの対応する各ペアの比較で、`True` が返される。

    たとえば、次の例では、`Equals` で `employee01` と `employee08` に対してのみ `True` が返されます。 各行の前のコメントは、新しいインスタンスが `employee01` と一致しない理由を示しています。

    [!code-vb[VbVbalrAnonymousTypes#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#24)]

- `GetHashcode` では、適切な一意の GetHashCode アルゴリズムが提供されます。 このアルゴリズムでは、キー プロパティのみを使用してハッシュ コードを計算します。

- `ToString` では、次の例に示すように、連結されたプロパティ値の文字列が返されます。 キーとキー以外のプロパティの両方が含まれます。

  [!code-vb[VbVbalrAnonymousTypes#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#29)]

匿名型の明示的に名前が付けられたプロパティは、生成されたこれらのメソッドと競合できません。 つまり、`.Equals`、`.GetHashCode`、`.ToString` を使用してプロパティの名前を指定することはできません。

少なくとも 1 つのキー プロパティを含む匿名型定義では、<xref:System.IEquatable%601?displayProperty=nameWithType> インターフェイスも実装します。ここで、`T` は匿名型の型です。

> [!NOTE]
> 匿名型の宣言では、同じアセンブリ内に存在する場合にのみ、同じ匿名型が作成され、そのプロパティの名前と推論される型は同じで、プロパティは同じ順序で宣言され、同じプロパティがキー プロパティとしてマークされます。

## <a name="see-also"></a>関連項目

- [匿名型](anonymous-types.md)
- [方法: 匿名型の宣言におけるプロパティ名と型を推論する](how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
