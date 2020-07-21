---
title: スコープ
ms.date: 07/20/2015
helpviewer_keywords:
- module scope [Visual Basic]
- scope [Visual Basic], levels
- module level
- procedures [Visual Basic], scope
- declared elements [Visual Basic], scope
- namespaces [Visual Basic], scope
- scope [Visual Basic], declared elements
- scope [Visual Basic], about scope
- levels of scope [Visual Basic]
- block scope [Visual Basic]
- scope [Visual Basic], Visual Basic
- procedure scope [Visual Basic]
ms.assetid: 208106fe-79c9-4eec-93c6-55f08548895f
ms.openlocfilehash: 1bee904996257474b7457b2aefb1f17d250933cb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410735"
---
# <a name="scope-in-visual-basic"></a>Visual Basic におけるスコープ

宣言された要素の*スコープ*は、その名前を修飾したり、[Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md) から使用できるようにしたりしなくても、それを参照できるすべてのコードのセットです。 要素には、次のいずれかのレベルのスコープを設定できます。

|レベル|説明|
|-----------|-----------------|
|ブロック スコープ|それが宣言されているコード ブロック内でのみ使用可能|
|プロシージャ スコープ|それが宣言されているプロシージャ内のすべてのコードで使用可能|
|モジュール スコープ|それが宣言されているモジュール、クラス、または構造体内のすべてのコードで使用可能|
|名前空間スコープ|それが宣言されている名前空間内のすべてのコードで使用可能|

これらのスコープのレベルは、最も狭い (ブロック) から最も広い (名前空間) まで進展します。ここで、*最も狭いスコープ*とは、修飾せずに要素を参照できる最小限のコードのセットを意味します。 詳細については、このページの「スコープのレベル」を参照してください。

## <a name="specifying-scope-and-defining-variables"></a>スコープの指定と変数の定義

要素のスコープは、それを宣言するときに指定します。 スコープは、次の要因によって異なる場合があります。

- 要素を宣言する領域 (ブロック、プロシージャ、モジュール、クラス、または構造体)

- 要素の宣言を含む名前空間

- 要素に対して宣言するアクセス レベル

同じ名前だがスコープが異なる変数を定義する場合は、それによって予期しない結果につながる可能性があるため、注意してください。 詳細については、「 [References to Declared Elements](references-to-declared-elements.md)」を参照してください。

## <a name="levels-of-scope"></a>スコープのレベル

プログラミング要素は、それを宣言する領域全体で使用できます。 同じリージョン内のすべてのコードでは、その名前を修飾せずに要素を参照できます。

### <a name="block-scope"></a>ブロック スコープ

ブロックは、次のように、開始と終了の宣言ステートメントに囲まれた一連のステートメントです。

- `Do` および `Loop`

- `For` [`Each`] および `Next`

- `If` および `End If`

- `Select` および `End Select`

- `SyncLock` および `End SyncLock`

- `Try` および `End Try`

- `While` および `End While`

- `With` および `End With`

ブロック内で変数を宣言すると、そのブロック内でのみそれを使用できます。 次の例で、整数変数 `cube` のスコープは `If` と `End If` の間のブロックであるため、実行がブロックから出ると、`cube` を参照できなくなります。

```vb
If n < 1291 Then
    Dim cube As Integer
    cube = n ^ 3
End If
```

> [!NOTE]
> 変数のスコープがブロックに制限されている場合でも、その有効期間はプロシージャ全体の有効期間になります。 プロシージャの実行中にブロックに複数回入る場合、各ブロック変数で前の値が保持されます。 そのような場合に予期しない結果を避けるには、ブロックの先頭でブロック変数を初期化することをお勧めします。

### <a name="procedure-scope"></a>プロシージャ スコープ

プロシージャ内で宣言された要素は、そのプロシージャの外部で使用できません。 宣言を含むプロシージャだけがそれを使用できます。 このレベルの変数は、*ローカル変数*とも呼ばれます。 それらは、[Dim ステートメント](../../../language-reference/statements/dim-statement.md)で、[Static](../../../language-reference/modifiers/static.md) キーワードを付けるか、または付けないで、宣言します。

プロシージャとブロックのスコープは密接に関連しています。 プロシージャ内の、ただしそのプロシージャ内のいずれかのブロックの外部で変数を宣言した場合、その変数はブロック スコープを持つと考えることができます。その場合ブロックはプロシージャ全体になります。

> [!NOTE]
> すべてのローカル要素は、`Static` 変数であっても、それらが存在するプロシージャに対してプライベートです。 プロシージャ内で [Public](../../../language-reference/modifiers/public.md) キーワードを使用して要素を宣言することはできません。

### <a name="module-scope"></a>モジュール スコープ

便宜上、*モジュール レベル*という 1 つの用語は、モジュール、クラス、および構造体に等しく適用されます。 このレベルで要素を宣言するには、宣言ステートメントをプロシージャまたはブロックの外部で、ただしモジュール、クラス、または構造体内に配置します。

モジュール レベルで宣言を行うと、選択したアクセス レベルによってスコープが決まります。 モジュール、クラス、または構造体を含む名前空間もスコープに影響します。

[Private](../../../language-reference/modifiers/private.md) アクセス レベルを宣言した要素は、そのモジュール内のすべてのプロシージャで使用できますが、別のモジュール内のコードでは使用できません。 アクセス レベル キーワードを使用しない場合、モジュール レベルの `Dim` ステートメントは既定で `Private` になります。 ただし、`Dim` ステートメントで `Private` キーワードを使用することで、スコープとアクセス レベルをより明確にすることができます。

次の例では、モジュールに定義されているすべてのプロシージャで、文字列変数 `strMsg` を参照できます。 2 番目のプロシージャを呼び出すと、ダイアログ ボックスに `strMsg` 文字列変数の内容が表示されます。

```vb
' Put the following declaration at module level (not in any procedure).
Private strMsg As String
' Put the following Sub procedure in the same module.
Sub initializePrivateVariable()
    strMsg = "This variable cannot be used outside this module."
End Sub
' Put the following Sub procedure in the same module.
Sub usePrivateVariable()
    MsgBox(strMsg)
End Sub
```

### <a name="namespace-scope"></a>名前空間スコープ

[Friend](../../../language-reference/modifiers/friend.md) または [Public](../../../language-reference/modifiers/public.md) キーワードを使用して、要素をモジュール レベルで宣言すると、その要素が宣言されている名前空間全体のすべてのプロシージャで使用できるようになります。 前の例を次のように変更すると、文字列変数 `strMsg` は、宣言の名前空間内の任意の場所でコードによって参照できます。

```vb
' Include this declaration at module level (not inside any procedure).
Public strMsg As String
```

名前空間スコープには、入れ子になった名前空間が含まれます。 名前空間内から使用できる要素は、その名前空間内に入れ子になっているすべての名前空間内からも使用できます。

プロジェクトに [Namespace ステートメント](../../../language-reference/statements/namespace-statement.md) が含まれていない場合、プロジェクトのすべてのものが同じ名前空間内にあります。 この場合、名前空間スコープはプロジェクト スコープと考えることができます。 モジュール、クラス、または構造体内の `Public` 要素は、そのプロジェクトを参照するすべてのプロジェクトでも使用できます。

## <a name="choice-of-scope"></a>スコープの選択

変数を宣言する場合、そのスコープを選択するときに、次の点に注意する必要があります。

### <a name="advantages-of-local-variables"></a>ローカル変数の利点

ローカル変数は、次の理由で、あらゆる種類の一時的な計算に適しています。

- **名前の競合の回避。** ローカル変数名は競合する可能性がありません。 たとえば、`intTemp` という変数を含む複数の異なるプロシージャを作成できます。 各 `intTemp` がローカル変数として宣言されている限り、各プロシージャではその独自のバージョンの `intTemp` のみが認識されます。 他のプロシージャの `intTemp` 変数に影響を与えることなく、あるプロシージャで、そのローカル `intTemp` の値を変更できます。

- **メモリの使用量。** ローカル変数は、プロシージャの実行中にのみメモリを消費します。 それらのメモリは、プロシージャが呼び出し元のコードに戻ったときに解放されます。 これに対し、[Shared](../../../language-reference/modifiers/shared.md) 変数と [Static](../../../language-reference/modifiers/static.md) 変数では、アプリケーションが実行を停止するまでメモリ リソースが消費されるため、必要な場合にのみそれらを使用してください。 *インスタンス変数*では、それらのインスタンスが存在し続ける間メモリが消費されるので、ローカル変数よりも非効率的ですが、`Shared` または `Static` 変数よりも効率的である可能性があります。

### <a name="minimizing-scope"></a>スコープの最小化

一般に、変数または定数を宣言するときは、スコープを可能な限り狭くすることをお勧めします (ブロック スコープが最も狭い)。 これにより、メモリを節約し、コードで間違った変数を誤って参照する可能性が最小限に抑えられます。 同様に、プロシージャ呼び出しの間でその値を保持する必要がある場合にのみ、変数を [Static](../../../language-reference/modifiers/static.md) として宣言する必要があります。

## <a name="see-also"></a>関連項目

- [宣言された要素の特性](declared-element-characteristics.md)
- [方法: 変数のスコープを制御する](how-to-control-the-scope-of-a-variable.md)
- [Visual Basic における有効期間](lifetime.md)
- [Visual Basic でのアクセス レベル](access-levels.md)
- [宣言された要素の参照](references-to-declared-elements.md)
- [変数宣言](../variables/variable-declaration.md)
