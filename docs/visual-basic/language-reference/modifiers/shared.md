---
title: Shared
ms.date: 07/20/2015
f1_keywords:
- vb.Shared
helpviewer_keywords:
- Shared keyword [Visual Basic]
- members [Visual Basic], shared
- shared members
- nonshared
- shared [elements VB]
- elements [Visual Basic], shared
ms.assetid: 2bf7cf2c-b0dd-485e-8749-b5d674dab4cd
ms.openlocfilehash: b51c88e1af3a720912af8ba6aaf8ae4016af9cfa
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990192"
---
# <a name="shared-visual-basic"></a>Shared (Visual Basic)

1 つ以上の宣言されたプログラミング要素が、クラスまたは構造体の特定のインスタンスではなく、クラスまたは構造体全体に関連付けられることを指定します。

## <a name="when-to-use-shared"></a>Shared を使用する場面

クラスまたは構造体のメンバーを共有すると、各インスタンスが独自のコピーを維持する*非共有*とは異なり、すべてのインスタンスでそれを使用できるようになります。 共有は、変数の値をアプリケーション全体に適用する場合などに便利です。 この変数を `Shared` として宣言すると、すべてのインスタンスが同じストレージの場所にアクセスするため、1 つのインスタンスで変数の値が変更されると、すべてのインスタンスが更新された値にアクセスするようになります。

共有によってメンバーのアクセス レベルが変更されることはありません。 たとえば、クラス メンバーには、共有とプライベート (クラス内からのみアクセス可能)、または非共有とパブリックを指定できます。 詳しくは、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

## <a name="rules"></a>ルール

- **宣言コンテキスト。** `Shared` は、モジュール レベルでのみ使用できます。 つまり、`Shared` 要素の宣言コンテキストは、クラスまたは構造体にする必要があり、ソース ファイル、名前空間、プロシージャにすることはできません。

- **結合された修飾子。** `Shared` は、同じ宣言内で、[Overrides](overrides.md)、[Overridable](overridable.md)、[NotOverridable](notoverridable.md)、[MustOverride](mustoverride.md)、または [Static](static.md) と一緒に指定することはできません。

- **アクセス。** 共有要素にアクセスするには、そのクラスまたは構造体の特定のインスタンスの変数名ではなく、そのクラスまたは構造体の名前で修飾します。 その共有メンバーにアクセスするために、クラスまたは構造体のインスタンスを作成する必要もありません。

     次の例では、<xref:System.Double> 構造体によって公開された <xref:System.Double.IsNaN%2A> 共有プロシージャを呼び出しています。

     ```vb
     If Double.IsNaN(result) Then Console.WriteLine("Result is mathematically undefined.")
     ```

- **暗黙的共有。** [Const ステートメント](../statements/const-statement.md)では `Shared` 修飾子を使用できませんが、定数は暗黙的に共有されます。 同様に、モジュールまたはインターフェイスのメンバーを `Shared` として宣言できませんが、それらは暗黙的に共有されます。

## <a name="behavior"></a>動作

- **ストレージ。** 共有変数またはイベントは、そのクラスまたは構造体の、作成するインスタンスの数に関係なく、メモリに 1 回だけ格納されます。 同様に、共有プロシージャまたはプロパティは、ローカル変数のセットを 1 つだけ保持します。

- **インスタンス変数によるアクセス。** 共有要素にアクセスするには、そのクラスまたは構造体の特定のインスタンスを格納する変数の名前でそれを修飾します。 これは通常、想定どおりに動作しますが、コンパイラでは警告メッセージが生成され、変数ではなくクラスまたは構造体の名前によってアクセスが行われます。

- **インスタンス式によるアクセス。** クラスまたは構造体のインスタンスを返す式によって共有要素にアクセスする場合、コンパイラでは、式を評価するのではなく、クラスまたは構造体の名前によってアクセスが行われます。 このアクセスにより、式でインスタンスを返すことに加えて、他のアクションを実行することを意図した場合に、予期しない結果が発生します。 この状況を次の例に示します。
  
    ```vb
    Sub Main()
        ' The following line is the preferred way to access Total.
        ShareTotal.Total = 10

        ' The following line generates a compiler warning message and
        ' accesses total through class ShareTotal instead of through
        ' the variable instanceVar. This works as expected and adds
        ' 100 to Total.
        Dim instanceVar As New ShareTotal
        instanceVar.Total += 100

        ' The following line generates a compiler warning message and
        ' accesses total through class ShareTotal instead of calling
        ' ReturnClass(). This adds 1000 to total but does not work as
        ' expected, because the WriteLine in ReturnClass() does not run.
        Console.WriteLine("Value of total is " & CStr(ShareTotal.Total))
        ReturnClass().Total += 1000
    End Sub

    Public Function ReturnClass() As ShareTotal
        Console.WriteLine("Function ReturnClass() called")
        Return New ShareTotal
    End Function

    Public Class ShareTotal
        Public Shared Property Total As Integer
    End Class
    ```

     前の例では、コードがインスタンス経由で共有プロパティ `Total` にアクセスするどちらのときも、コンパイラによって警告メッセージが生成されます。 いずれの場合も、クラス `ShareTotal` 経由で直接アクセスが行われ、インスタンスが使用されません。 プロシージャ `ReturnClass` への意図した呼び出しの場合、これは `ReturnClass` への呼び出しも生成されないことを意味するため、"Function ReturnClass() called" を表示する追加のアクションが実行されません。

`Shared` 修飾子は、次のコンテキストで使用できます。

- [Dim ステートメント](../statements/dim-statement.md)
- [Event ステートメント](../statements/event-statement.md)
- [Function ステートメント](../statements/function-statement.md)
- [Operator ステートメント](../statements/operator-statement.md)
- [Property ステートメント](../statements/property-statement.md)
- [Sub ステートメント](../statements/sub-statement.md)
  
## <a name="see-also"></a>関連項目

- [Shadows](shadows.md)
- [Static](static.md)
- [Visual Basic における有効期間](../../programming-guide/language-features/declared-elements/lifetime.md)
- [手順](../../programming-guide/language-features/procedures/index.md)
- [構造体](../../programming-guide/language-features/data-types/structures.md)
- [クラスとオブジェクト](../../programming-guide/language-features/objects-and-classes/index.md)
