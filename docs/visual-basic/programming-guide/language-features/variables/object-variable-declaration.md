---
title: オブジェクト変数の宣言
ms.date: 07/20/2015
helpviewer_keywords:
- early binding [Visual Basic]
- declarations [Visual Basic], class
- classes [Visual Basic], declaring
- binding [Visual Basic], late and early
- object variables [Visual Basic], declaring
- variables [Visual Basic], object
- declaring variables [Visual Basic], object variables
- declaring classes [Visual Basic]
- late binding [Visual Basic]
ms.assetid: 2a5a41a3-1aa8-4236-b1f0-2382af7bf715
ms.openlocfilehash: b6de52cf738a56a42c82978b54cef31574ab0bcb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410362"
---
# <a name="object-variable-declaration-visual-basic"></a>オブジェクト変数の宣言 (Visual Basic)
通常の宣言ステートメントを使用して、オブジェクト変数を宣言します。 データ型については、`Object` (つまり、[Object データ型](../../../language-reference/data-types/object-data-type.md)) またはオブジェクトの作成元となるより具体的なクラスを指定します。  
  
 変数を `Object` として宣言することは、<xref:System.Object?displayProperty=nameWithType> として宣言することと同じです。  
  
 特定のオブジェクト クラスを使用して変数を宣言すると、そのクラスによって公開されているすべてのメソッドとプロパティ、およびそのクラスを継承しているクラスに変数でアクセスすることができます。 <xref:System.Object> を使用して変数を宣言すると、`Option Strict Off` にして遅延バインディングを許可しない限り、その変数がアクセスできるのは、<xref:System.Object> クラスのメンバーだけです。  
  
## <a name="declaration-syntax"></a>宣言の構文  
 オブジェクト変数を宣言するには、次の構文を使用します。  
  
```vb  
Dim variablename As [New] { objectclass | Object }  
```  
  
 宣言で [Public](../../../language-reference/modifiers/public.md)、[Protected](../../../language-reference/modifiers/protected.md)、[Friend](../../../language-reference/modifiers/friend.md)、`Protected Friend`、[Private](../../../language-reference/modifiers/private.md)、[Shared](../../../language-reference/modifiers/shared.md)、[Static](../../../language-reference/modifiers/static.md) のいずれかを指定することもできます。 次の宣言の例は有効です。  
  
```vb  
Private objA As Object  
Static objB As System.Windows.Forms.Label  
Dim objC As System.OperatingSystem  
```  
  
## <a name="late-binding-and-early-binding"></a>遅延バインディングと事前バインディング  
 場合によっては、コードを実行するまで特定のクラスが不明な場合があります。 この場合は、`Object` データ型を使用して、オブジェクト変数を宣言する必要があります。 これにより、オブジェクトの任意の型への一般的な参照が作成され、特定のクラスが実行時に割り当てられます。 これは "*遅延バインディング*" と呼ばれます。 遅延バインディングでは、追加の実行時間が必要です。 また、コードは、最後に割り当てたクラスのメソッドとプロパティに限定されます。 これにより、コードが別のクラスのメンバーにアクセスしようとした場合に、実行時エラーが発生する可能性があります。  
  
 コンパイル時に特定のクラスがわかっている場合は、そのクラスのオブジェクト変数を宣言する必要があります。 これは、*事前バインディング*と呼ばれます。 事前バインディングにより、パフォーマンスが向上し、コードが特定のクラスのすべてのメソッドとプロパティにアクセスできるようになります。 前の例の宣言では、変数 `objA` がクラス <xref:System.Windows.Forms.Label?displayProperty=nameWithType> のオブジェクトのみを使用する場合、その宣言で `As System.Windows.Forms.Label` を指定する必要があります。  
  
### <a name="advantages-of-early-binding"></a>事前バインディングの利点  
 オブジェクト変数を特定のクラスとして宣言することには、いくつかの利点があります。  
  
- 自動型チェック  
  
- 特定のクラスのすべてのメンバーへのアクセスが保証される  
  
- コード エディターでの Microsoft IntelliSense のサポート  
  
- コードの読みやすさの向上  
  
- コード内のエラーの数が減る  
  
- 実行時ではなくコンパイル時にエラーが見つかる  
  
- コード実行の高速化  
  
## <a name="access-to-object-variable-members"></a>オブジェクト変数メンバーへのアクセス  
 `Option Strict` が `On` になっている場合に、オブジェクト変数がアクセスできるのは、それを宣言するときに指定したクラスのメソッドとプロパティだけです。 次に例を示します。  
  
```vb  
' Option statements must precede all other source file lines.  
Option Strict On  
' Imports statement must precede all declarations in the source file.  
Imports System.Windows.Forms  
Public Sub accessMembers()  
    Dim p As Object  
    Dim q As System.Windows.Forms.Label  
    p = New System.Windows.Forms.Label  
    q = New System.Windows.Forms.Label  
    Dim j, k As Integer  
    ' The following statement generates a compiler ERROR.  
    j = p.Left  
    ' The following statement retrieves the left edge of the label in pixels.  
    k = q.Left  
End Sub  
```  
  
 この例の場合、 `p` で使用できるのは <xref:System.Object> クラス自体のメンバーのみです。 `Left` プロパティは含まれません。 一方、 `q` は、 <xref:System.Windows.Forms.Label>型として宣言されているため、 <xref:System.Windows.Forms.Label> 名前空間の <xref:System.Windows.Forms> クラスのすべてのメソッドとプロパティを使用できます。  
  
## <a name="flexibility-of-object-variables"></a>オブジェクト変数の柔軟性  
 継承階層内のオブジェクトを操作する場合は、オブジェクト変数の宣言に使用するクラスを選択できます。 この選択を行うには、オブジェクトの割り当ての柔軟性と、クラスのメンバーへのアクセスとのバランスを取る必要があります。 たとえば、<xref:System.Windows.Forms.Form?displayProperty=nameWithType> クラスにつながる継承階層を考えてみます。  
  
 <xref:System.Object>  
  
 &nbsp;&nbsp;<xref:System.MarshalByRefObject>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;<xref:System.ComponentModel.Component>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.Windows.Forms.Control>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.Windows.Forms.ScrollableControl>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.Windows.Forms.ContainerControl>  
  
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<xref:System.Windows.Forms.Form>  
  
 アプリケーションで、クラス <xref:System.Windows.Forms.Form> から継承される `specialForm` というフォーム クラスが定義されているとします。 次の例に示すように、明確に `specialForm` を参照するオブジェクト変数を宣言できます。  
  
```vb  
Public Class specialForm  
    Inherits System.Windows.Forms.Form  
    ' Insert code defining methods and properties of specialForm.  
End Class  
Dim nextForm As New specialForm  
```  
  
 上記の例の宣言では、変数 `nextForm` を `specialForm` クラスのオブジェクトに限定していますが、`specialForm` のすべてのメソッドとプロパティが、`nextForm` と、`specialForm` の継承元のすべてのクラスのすべてのメンバーで使用できるようになります。  
  
 次の例に示すように、オブジェクト変数は、<xref:System.Windows.Forms.Form> 型になるように宣言することで、より一般的なものにすることができます。  
  
```vb  
Dim anyForm As System.Windows.Forms.Form  
```  
  
 上記の例の宣言により、アプリケーションの任意のフォームを `anyForm` に割り当てることができます。 ただし、`anyForm` はクラス <xref:System.Windows.Forms.Form> のすべてのメンバーにアクセスできますが、`specialForm` などの特定のフォームに対して定義されている追加のメソッドやプロパティを使用することはできません。  
  
 基底クラスのすべてのメンバーは派生クラスで使用できますが、派生クラスの追加メンバーを基底クラスで使用することはできません。  
  
## <a name="see-also"></a>関連項目

- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の代入](object-variable-assignment.md)
- [オブジェクト変数の値](object-variable-values.md)
- [方法: Visual Basic でオブジェクト変数を宣言し、オブジェクト変数にオブジェクトを代入する](how-to-declare-an-object-variable-and-assign-an-object-to-it.md)
- [方法: オブジェクトのメンバーにアクセスする](how-to-access-members-of-an-object.md)
- [New 演算子](../../../language-reference/operators/new-operator.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
- [ローカル型の推論](local-type-inference.md)
