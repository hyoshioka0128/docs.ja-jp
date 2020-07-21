---
title: 継承の基本
ms.date: 07/20/2015
helpviewer_keywords:
- derived classes [Visual Basic], inheritance
- MyClass keyword [Visual Basic], using
- MyBase keyword [Visual Basic], using
- Inherits statement [Visual Basic], inheritance
- overriding, Overridable keyword
- MustInherit keyword [Visual Basic], using
- Overrides keyword [Visual Basic], using
- inheritance
- MustInherit classes [Visual Basic]
- MustOverride keyword [Visual Basic], using
- classes [Visual Basic], derived
- NotInheritable keyword [Visual Basic], using
- base classes [Visual Basic], extending properties and methods [Visual Basic]
- NotOverridable keyword [Visual Basic], using
- base classes [Visual Basic], inheritance
- abstract classes [Visual Basic], inheritance
- overriding, Overrides keyword
ms.assetid: dfc8deba-f5b3-4d1d-a937-7cb826446fc5
ms.openlocfilehash: 3bf1847f618a642d26df4aa1c5247a4ba2bd3b23
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411780"
---
# <a name="inheritance-basics-visual-basic"></a>継承の基本 (Visual Basic)

`Inherits` ステートメントは、*基底クラス*と呼ばれる既存のクラスに基づいて、*派生クラス*と呼ばれる新しいクラスを宣言するために使用されます。 派生クラスは、基底クラスで定義されているプロパティ、メソッド、イベント、フィールド、および定数を継承し、これらを拡張することができます。 次のセクションでは、継承に関するいくつかの規則と、クラスが継承したり継承されたりする方法を変更するために使用できる修飾子について説明します。

- 既定では、`NotInheritable` キーワードでマークされていない限り、すべてのクラスが継承可能です。 クラスは、プロジェクト内の他のクラスから、またはプロジェクトが参照する他のアセンブリのクラスから継承できます。

- 複数の継承を許可する言語とは異なり、Visual Basic ではクラスでの単一継承のみが許可されます。つまり、派生クラスは基底クラスを 1 つだけ持つことができます。 クラスでは複数の継承は許可されませんが、クラスは複数のインターフェイスを実装できます。これにより、同じ目的を効率的に実現できます。

- 基底クラスで制限された項目を公開しないようにするには、派生クラスのアクセスの種類がその基底クラスと同等以上に制限されている必要があります。 たとえば、`Public` クラスは、`Friend` または `Private` クラスを継承できず、`Friend` クラスは `Private` クラスを継承できません。

## <a name="inheritance-modifiers"></a>継承修飾子

Visual Basic では、継承をサポートするために、次のクラスレベルのステートメントと修飾子が導入されています。

- `Inherits` ステートメント - 基底クラスを指定します。

- `NotInheritable` 修飾子 - プログラマがクラスを基底クラスとして使用できないようにします。

- `MustInherit` 修飾子 - クラスが基底クラスとしてのみ使用されることを指定します。 `MustInherit` クラスのインスタンスを直接作成することはできません。派生クラスの基底クラスのインスタンスとしてのみ作成できます。 (C++ や C# などの他のプログラミング言語では、このようなクラスについて説明するのに*抽象クラス*という用語を使用します。)

## <a name="overriding-properties-and-methods-in-derived-classes"></a>派生クラスのプロパティとメソッドのオーバーライド

既定では、派生クラスは基底クラスのプロパティとメソッドを継承します。 派生クラス内の継承されたプロパティまたはメソッドの動作が異なる場合は、*オーバーライド*できます。 つまり、派生クラスにメソッドの新しい実装を定義できます。 プロパティやメソッドのオーバーライド方法を制御するには、次の修飾子を使用します。

- `Overridable` - クラス内のプロパティまたはメソッドを派生クラスでオーバーライドできます。

- `Overrides` - 基底クラスに定義された `Overridable` プロパティまたはメソッドをオーバーライドします。

- `NotOverridable` - 継承するクラスでプロパティまたはメソッドがオーバーライドされないようにします。 既定では、`Public` メソッドは `NotOverridable` です。

- `MustOverride` - 派生クラスでプロパティまたはメソッドをオーバーライドする必要があります。 `MustOverride` キーワードを使用する場合、メソッド定義は、`Sub`、`Function`、または `Property` ステートメントだけで構成されます。 他のステートメントは許可されません。具体的には、`End Sub` または `End Function` ステートメントはありません。 `MustOverride` メソッドは `MustInherit` クラスで宣言する必要があります。

給与支払いを処理するクラスを定義するとします。 典型的な 1 週間の給与を計算する `RunPayroll` メソッドを含むジェネリック `Payroll` クラスを定義できます。 その後、より特殊化された `BonusPayroll` クラスの基底クラスとして `Payroll` を使用できます。これは、従業員の賞与を配分するときに使用できます。

`BonusPayroll` クラスは、基底クラス `Payroll` で定義されている `PayEmployee` メソッドを継承し、オーバーライドできます。

次の例では、基底クラス `Payroll,` と、継承されたメソッド `PayEmployee` をオーバーライドする派生クラス `BonusPayroll` を定義しています。 プロシージャ `RunPayroll` は、`Payroll` オブジェクトと `BonusPayroll` オブジェクトを作成してから、両方のオブジェクトの `PayEmployee` メソッドを実行する関数 `Pay` に渡します。

[!code-vb[VbVbalrOOP#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#28)]

## <a name="the-mybase-keyword"></a>MyBase キーワード

`MyBase` キーワードは、クラスの現在のインスタンスの基底クラスを参照するオブジェクト変数のように動作します。 `MyBase` は、派生クラスでオーバーライドまたはシャドウされた基底クラスのメンバーにアクセスするためによく使用されます。 特に、`MyBase.New` は、派生クラスのコンストラクターから基底クラスのコンストラクターを明示的に呼び出すために使用されます。

たとえば、基底クラスから継承されたメソッドをオーバーライドする派生クラスを設計するとします。 オーバーライドされたメソッドは、次のコード フラグメントに示されている、基底クラスのメソッドを呼び出して、戻り値を変更することができます。

[!code-vb[VbVbalrOOP#109](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#109)]

`MyBase` の使用に関する制限事項を次の一覧に示します。

- `MyBase` は、直接の基底クラスとその継承メンバーを参照します。 クラス内の `Private` メンバーへのアクセスには使用できません。

- `MyBase` はキーワードであり、実際のオブジェクトではありません。 `MyBase` は、変数に割り当てたり、プロシージャに渡したり、`Is` の比較で使用したりすることはできません。

- `MyBase` で修飾されるメソッドは、直接の基底クラスで定義されている必要はありません。代わりに、間接的に継承された基底クラスで定義することができます。 `MyBase` によって修飾された参照を正しくコンパイルするために、一部の基底クラスには、呼び出しに存在するパラメーターの名前と型に一致するメソッドが含まれている必要があります。

- `MyBase` を使用して `MustOverride` 基底クラスのメソッドを呼び出すことはできません。

- `MyBase` を使用してそれ自体を修飾することはできません。 したがって、次のコードは有効ではありません。

  `MyBase.MyBase.BtnOK_Click()`

- `MyBase` はモジュールでは使用できません。

- `MyBase` は、基底クラスが別のアセンブリにある場合に `Friend` としてマークされている基底クラスのメンバーにアクセスするために使用することはできません。

詳細ともう 1 つの例については、「[方法: 派生クラスによって非表示になっている変数にアクセスする](../declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)」を参照してください。

## <a name="the-myclass-keyword"></a>MyClass キーワード

`MyClass` キーワードは、もともと実装されているクラスの現在のインスタンスを参照するオブジェクト変数と同様に動作します。 `MyClass` は `Me` に似ていますが、`MyClass` のすべてのメソッドとプロパティ呼び出しは、メソッドまたはプロパティが [NotOverridable](../../../language-reference/modifiers/notoverridable.md) であるかのように扱われます。 したがって、メソッドまたはプロパティは、派生クラスでのオーバーライドによる影響を受けません。

- `MyClass` はキーワードであり、実際のオブジェクトではありません。 `MyClass` は、変数に割り当てたり、プロシージャに渡したり、`Is` の比較で使用したりすることはできません。

- `MyClass` は、含まれているクラスとその継承メンバーを参照します。

- `MyClass` は `Shared` メンバーの修飾子として使用できます。

- `MyClass` は `Shared` メソッド内では使用できませんが、インスタンス メソッド内で使用して、クラスの共有メンバーにアクセスすることができます。

- `MyClass` は標準モジュールでは使用できません。

- `MyClass` は、基底クラスで定義されていて、そのクラスで提供されるメソッドの実装を持たないメソッドを修飾するために使用できます。 このような参照は、`MyBase.`*メソッド*と同じ意味を持ちます。

次の例では、`Me` と `MyClass` を比較します。

```vb
Class baseClass
    Public Overridable Sub testMethod()
        MsgBox("Base class string")
    End Sub
    Public Sub useMe()
        ' The following call uses the calling class's method, even if
        ' that method is an override.
        Me.testMethod()
    End Sub
    Public Sub useMyClass()
        ' The following call uses this instance's method and not any
        ' override.
        MyClass.testMethod()
    End Sub
End Class
Class derivedClass : Inherits baseClass
    Public Overrides Sub testMethod()
        MsgBox("Derived class string")
    End Sub
End Class
Class testClasses
    Sub startHere()
        Dim testObj As derivedClass = New derivedClass()
        ' The following call displays "Derived class string".
        testObj.useMe()
        ' The following call displays "Base class string".
        testObj.useMyClass()
    End Sub
End Class
```

`derivedClass` が `testMethod` をオーバーライドしても、`useMyClass` の `MyClass` キーワードがオーバーライドの効果を無効にし、コンパイラは `testMethod` の基底クラスのバージョンの呼び出しを解決します。

## <a name="see-also"></a>関連項目

- [Inherits ステートメント](../../../language-reference/statements/inherits-statement.md)
- [Me、My、MyBase、および MyClass](../../program-structure/me-my-mybase-and-myclass.md)
