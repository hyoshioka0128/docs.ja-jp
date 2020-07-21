---
title: Dim ステートメント
ms.date: 05/12/2018
f1_keywords:
- vb.Dim
- Dim
helpviewer_keywords:
- Public keyword [Visual Basic], in Dim statement
- Dim statement [Visual Basic]
- fixed-length strings [Visual Basic], declaring
- variables [Visual Basic], declaring
- WithEvents keyword [Visual Basic], Dim statement
- dynamic arrays [Visual Basic], Dim statement
- variables [Visual Basic], initializing
- '{} braces'
- fields [Visual Basic], as member variables
- declarations [Visual Basic], dynamic arrays
- member variables [Visual Basic]
- default values [Visual Basic]
- data types [Visual Basic], assigning
- braces {}
- As keyword [Visual Basic], in Dim statement
- arrays [Visual Basic], declaring
- New keyword [Visual Basic], Dim statement
- To keyword [Visual Basic], in Dim statement
- storage [Visual Basic], allocating
- local variables [Visual Basic]
- declaration statements [Visual Basic]
- Dim statement [Visual Basic], syntax
- variables [Visual Basic], member and local
ms.assetid: fae3eca1-f0b2-4400-994b-7aa58a848448
ms.openlocfilehash: 1b0c3089c366c417af926c8c0703cea021674432
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76744729"
---
# <a name="dim-statement-visual-basic"></a>Dim ステートメント (Visual Basic)

1 つ以上の変数に対して、宣言して記憶域を割り当てます。

## <a name="syntax"></a>構文

```vb
[ <attributelist> ] [ accessmodifier ] [[ Shared ] [ Shadows ] | [ Static ]] [ ReadOnly ]
Dim [ WithEvents ] variablelist
```

## <a name="parts"></a>指定項目

- `attributelist`

  任意。 「[属性リスト](attribute-list.md)」を参照してください。

- `accessmodifier`

  任意。 次のいずれかの値を指定します。

  - [Public](../modifiers/public.md)

  - [Protected](../modifiers/protected.md)

  - [Friend](../modifiers/friend.md)

  - [Private](../modifiers/private.md)

  - [Protected Friend](../modifiers/protected-friend.md)

  - [Private Protected](../modifiers/private-protected.md)

  「 [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

- `Shared`

  任意。 「[Shared](../modifiers/shared.md)」を参照してください。

- `Shadows`

  任意。 「[Shadows](../modifiers/shadows.md)」を参照してください。

- `Static`

  任意。 「[Static](../modifiers/static.md)」を参照してください。

- `ReadOnly`

  任意。 「[ReadOnly](../modifiers/readonly.md)」を参照してください。

- `WithEvents`

  任意。 これらが、イベントを生成できるクラスのインスタンスを参照するオブジェクト変数であることを指定します。 「[WithEvents](../modifiers/withevents.md)」を参照してください。

- `variablelist`

  必須です。 このステートメントで宣言されている変数の一覧。

  `variable [ , variable ... ]`

  `variable` の構文と指定項目は次のとおりです。

  `variablename [ ( [ boundslist ] ) ] [ As [ New ] datatype [ With`{`[ .propertyname = propinitializer [ , ... ] ] } ] ] [ = initializer ]`

  |パーツ|説明|
  |---|---|
  |`variablename`|必須です。 変数名。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。|
  |`boundslist`|任意。 配列変数の各次元の境界の一覧。|
  |`New`|任意。 `Dim` ステートメントの実行時にクラスの新しいインスタンスを作成します。|
  |`datatype`|任意。 変数のデータ型。|
  |`With`|任意。 オブジェクト初期化子の一覧を取り込みます。|
  |`propertyname`|任意。 インスタンスを作成しているクラスのプロパティの名前。|
  |`propinitializer`|`propertyname` = の後に必要です。 評価され、プロパティ名に割り当てられる式。|
  |`initializer`|`New` が指定されていない場合は省略可能です。 作成時に評価され、変数に割り当てられる式。|

## <a name="remarks"></a>Remarks

Visual Basic コンパイラでは、`Dim` ステートメントを使用して、変数のデータ型やその他の情報 (変数にアクセスできるコードなど) が判断されます。 次の例では、`Integer` 値を保持する変数を宣言しています。

```vb
Dim numberOfStudents As Integer
```

任意のデータ型や、列挙、構造体、クラス、またはインターフェイスの名前を指定できます。

```vb
Dim finished As Boolean
Dim monitorBox As System.Windows.Forms.Form
```

参照型の場合、`New` キーワードを使用して、データ型で指定されたクラスまたは構造体の新しいインスタンスを作成します。 `New` を使用する場合、初期化子式は使用しません。 代わりに、変数の作成元のクラスのコンストラクターに、必要に応じて、引数を指定します。

```vb
Dim bottomLabel As New System.Windows.Forms.Label
```

プロシージャ、ブロック、クラス、構造体、またはモジュールで変数を宣言できます。 ソース ファイル、名前空間、またはインターフェイスで変数を宣言することはできません。 詳細については、「[宣言コンテキストと既定のアクセス レベル](declaration-contexts-and-default-access-levels.md)」を参照してください。

プロシージャの外部のモジュール レベルで宣言されている変数は、*メンバー変数*または*フィールド*です。 メンバー変数のスコープは、クラス、構造体、またはモジュール全体になります。 プロシージャ レベルで宣言された変数は、*ローカル変数*です。 ローカル変数のスコープは、それらのプロシージャまたはブロック内のみになります。

プロシージャの外部で変数を宣言するために、次のアクセス修飾子を使用します。`Public`、`Protected`、`Friend`、`Protected Friend`、`Private`。 詳しくは、「[Visual Basic でのアクセス レベル](../../programming-guide/language-features/declared-elements/access-levels.md)」を参照してください。

`Dim` キーワードは省略可能で、通常、次のいずれかの修飾子を指定する場合は省略します。`Public`、`Protected`、`Friend`、`Protected Friend`、`Private`、`Shared`、`Shadows`、`Static`、`ReadOnly`、`WithEvents`。

```vb
Public maximumAllowed As Double
Protected Friend currentUserName As String
Private salary As Decimal
Static runningTotal As Integer
```

`Option Explicit` が on (既定値) の場合、コンパイラでは使用するすべての変数の宣言が必要になります。 詳細については、「[Option Explicit ステートメント](option-explicit-statement.md)」を参照してください。

## <a name="specifying-an-initial-value"></a>初期値の指定

変数を作成するときに、変数に値を割り当てることができます。 値型の場合は、*初期化子*を使用して、変数に割り当てる式を指定します。 式は、コンパイル時に計算可能な定数に評価される必要があります。

```vb
Dim quantity As Integer = 10
Dim message As String = "Just started"
```

初期化子が指定されていて、`As` 句でデータ型が指定されていない場合、*型の推定* が使用され、初期化子からデータ型が推定されます。 次の例では、`num1` と `num2` はどちらも整数として厳密に型指定されます。 2 つ目の宣言では、型の推定によって値 3 から型が推定されています。

```vb
' Use explicit typing.
Dim num1 As Integer = 3

' Use local type inference.
Dim num2 = 3
```

型の推定は、プロシージャ レベルで適用されます。 クラス、構造体、モジュール、またはインターフェイス内のプロシージャの外側には適用されません。 型の推定の詳細については、「[Option Infer ステートメント](option-infer-statement.md)」と「[ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)」を参照してください。

データ型または初期化子が指定されていない場合の動作については、このトピックで後述する「[既定のデータ型と値](dim-statement.md#default)」を参照してください。

*オブジェクト初期化子*を使用すると、名前付き型と匿名型のインスタンスを宣言できます。 次のコードでは、`Student` クラスのインスタンスを作成し、オブジェクト初期化子を使用してプロパティを初期化しています。

```vb
Dim student1 As New Student With {.First = "Michael",
                                  .Last = "Tucker"}
```

オブジェクト初期化子の詳細については、「[方法:オブジェクト初期化子を使用してオブジェクトを宣言する](../../programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)」、「[オブジェクト初期化子:名前付き型と匿名型](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)」、「[匿名型](../../programming-guide/language-features/objects-and-classes/anonymous-types.md)」を参照してください。

## <a name="declaring-multiple-variables"></a>複数の変数の宣言

1 つの宣言ステートメントで複数の変数を宣言し、それぞれに変数名を指定して、その後にかっこで囲んだ各配列名を指定できます。 複数の変数を指定するときは、コンマで区切ります。

```vb
Dim lastTime, nextTime, allTimes() As Date
```

1 つの `As` 句で複数の変数を宣言する場合、その変数のグループの初期化子を指定することはできません。

宣言する変数ごとに個別の `As` 句を使用して、異なる変数に異なるデータ型を指定できます。 各変数は、`variablename` 部分の後に最初に検出される `As` 句に指定されたデータ型を受け取ります。

```vb
Dim a, b, c As Single, x, y As Double, i As Integer
' a, b, and c are all Single; x and y are both Double
```

## <a name="arrays"></a>配列

複数の値を保持できる*配列*を保持する変数を宣言できます。 変数で配列を保持するように指定するには、その `variablename` の直後にかっこで囲んで続けます。 配列の詳細については、「[配列](../../programming-guide/language-features/arrays/index.md)」を参照してください。

配列の各次元の下限と上限を指定できます。 これを行うには、`boundslist` をかっこ内に含めます。 次元ごとに、`boundslist` では上限を指定し、必要に応じて下限を指定します。 下限は、指定したかどうかにかかわらず、常に 0 になります。 各インデックスは、0 から上限値までさまざまに異なる可能性があります。

次の 2 つのステートメントは同等です。 各ステートメントでは、21 個の `Integer` 要素の配列を宣言しています。 配列にアクセスする場合、インデックスは 0 から 20 まででさまざまに異なる可能性があります。

```vb
Dim totals(20) As Integer
Dim totals(0 To 20) As Integer
```

次のステートメントでは、`Double` 型の 2 次元配列を宣言しています。 配列には、それぞれ 6 列 (5 + 1) の 4 行 (3 + 1) があります。 上限は、次元の長さではなく、インデックスの最大有効値を表します。 次元の長さは、上限に 1 を加えた値です。

```vb
Dim matrix2(3, 5) As Double
```

配列には、1 から 32 の次元を指定できます。

配列宣言では、すべての境界を空白のままにできます。 こうすると、配列に指定した数の次元が設定されますが、初期化されません。 それは、少なくともその要素の一部を初期化するまで、`Nothing` の値になります。 `Dim` ステートメントでは、すべての次元に対して、または次元なしで、境界を指定する必要があります。

```vb
' Declare an array with blank array bounds.
Dim messages() As String
' Initialize the array.
ReDim messages(4)
```

配列に複数の次元がある場合は、次元の数を示すために、かっこの間にコンマを含める必要があります。

```vb
Dim oneDimension(), twoDimensions(,), threeDimensions(,,) As Byte
```

配列の次元の 1 つを -1 として宣言することによって、*長さゼロの配列*を宣言できます。 長さゼロの配列を保持する変数の値は、`Nothing` になりません。 特定の共通言語ランタイム関数では、長さゼロの配列が必要です。 このような配列にアクセスしようとすると、ランタイム例外が発生します。 詳細については、「[配列](../../programming-guide/language-features/arrays/index.md)」を参照してください。

配列の値を初期化するには、配列リテラルを使用します。 これを行うには、初期化値を中かっこ (`{}`) で囲みます。

```vb
Dim longArray() As Long = {0, 1, 2, 3}
```

多次元配列の場合、各個別の次元の初期化は外側の次元で中かっこで囲みます。 要素は、行優先順で指定します。

```vb
Dim twoDimensions(,) As Integer = {{0, 1, 2}, {10, 11, 12}}
```

配列リテラルの詳細については、「[配列](../../programming-guide/language-features/arrays/index.md)」を参照してください。

## <a name="default-data-types-and-values"></a><a name="default"></a> 既定のデータ型と値

次の表では、`Dim` ステートメントのデータ型と初期化子を指定するさまざまな組み合わせの結果を示します。

|データ型が指定されているか|初期化子が指定されているか|例|結果|
|---|---|---|---|
|いいえ|いいえ|`Dim qty`|[Option Strict](option-strict-statement.md) が off (既定値) の場合、変数は `Nothing` に設定されます。<br /><br /> `Option Strict` がオンの場合、コンパイル時エラーが発生します。|
|いいえ|はい|`Dim qty = 5`|[Option Infer](option-infer-statement.md) が on (既定値) の場合、変数は初期化子のデータ型になります。 「[ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)」を参照してください。<br /><br /> `Option Infer` がオフで、`Option Strict` がオフの場合、変数は `Object` のデータ型になります。<br /><br /> `Option Infer` がオフで、`Option Strict` がオンの場合、コンパイル時エラーが発生します。|
|はい|いいえ|`Dim qty As Integer`|変数は、データ型の既定値に初期化されます。 このセクションの後の方の表を参照してください。|
|はい|はい|`Dim qty  As Integer = 5`|初期化子のデータ型を指定したデータ型に変換できない場合は、コンパイル時エラーが発生します。|

データ型を指定しても初期化子を指定しない場合、Visual Basic によって、変数がそのデータ型の既定値に初期化されます。 次の表に既定の初期化値を示します。

|データの種類|既定値|
|---|---|
|すべての数値型 (`Byte` と `SByte` を含む)|0|
|`Char`|バイナリ 0|
|すべての参照型 (`Object`、`String`、すべての配列を含む)|`Nothing`|
|`Boolean`|`False`|
|`Date`|1 年 1 月 1 日の午前 12 時 (01/01/0001 12:00:00 AM)|

構造体の各要素は、個別の変数であるかのように初期化されます。 配列の長さを宣言しても、その要素を初期化しない場合、各要素は個別の変数であるかのように初期化されます。

## <a name="static-local-variable-lifetime"></a>静的ローカル変数の有効期間

`Static` ローカル変数の有効期間は、宣言されているプロシージャよりも長くなります。 変数の有効期間の境界は、プロシージャが宣言されている場所とそれが `Shared` かどうかによって異なります。

|プロシージャ宣言|変数が初期化される|変数の存在が停止する|
|---|---|---|
|モジュール内|プロシージャが初めて呼び出されたとき|プログラムの実行が停止したとき|
|クラスまたは構造体内、プロシージャは `Shared` である|特定のインスタンスか、またはクラスや構造体自体で、プロシージャが最初に呼び出されたとき|プログラムの実行が停止したとき|
|クラスまたは構造体内、プロシージャは `Shared` でない|特定のインスタンスで最初にプロシージャが呼び出されたとき|ガベージ コレクション (GC) のためにインスタンスが解放されたとき|

## <a name="attributes-and-modifiers"></a>属性と修飾子

属性は、ローカル変数ではなくメンバー変数にのみ適用できます。 属性は、アセンブリのメタデータに情報を提供します。これは、ローカル変数などの一時ストレージには意味がありません。

モジュール レベルでは、`Static` 修飾子を使用して、メンバー変数を宣言することはできません。 プロシージャ レベルで、`Shared`、`Shadows`、`ReadOnly`、`WithEvents`、または任意のアクセス修飾子を使用して、ローカル変数を宣言することはできません。

`accessmodifier` を指定することによって、変数にアクセスできるコードを指定できます。 クラスおよびモジュール メンバー変数 (プロシージャの外部) の既定は、プライベート アクセスに設定され、構造体メンバー変数の既定は、パブリック アクセスに設定されます。 アクセス修飾子を使用してこれらのアクセス レベルを調整できます。 ローカル変数 (プロシージャ内) では、アクセス修飾子を使用できません。

`WithEvents` は、プロシージャ内のローカル変数ではなく、メンバー変数に対してのみ指定できます。 `WithEvents` を指定する場合、変数のデータ型は、`Object` ではなく、特定のクラス型にする必要があります。 `WithEvents` で配列を宣言することはできません。 イベントの詳細については、「[イベント](../../programming-guide/language-features/events/index.md)」を参照してください。

> [!NOTE]
> クラス、構造体、またはモジュールの外部のコードでは、メンバー変数の名前を、そのクラス、構造体、またはモジュールの名前で修飾する必要があります。 プロシージャまたはブロックの外部のコードでは、そのプロシージャまたはブロック内のローカル変数を参照することはできません。

## <a name="releasing-managed-resources"></a>管理対象リソースの解放

.NET Framework ガベージ コレクターによって、ユーザー側の追加のコーディングなしで管理対象リソースが破棄されます。 ただし、ガベージ コレクターを待つことなく、管理対象リソースを強制的に破棄することができます。

クラスで特に貴重で少ないリソース (データベース接続やファイル ハンドルなど) が保持されている場合、次のガベージ コレクションによって使用されなくなったクラス インスタンスがクリーンアップされるまで待ちたくないことがあります。 クラスでは、<xref:System.IDisposable> インターフェイスを実装して、ガベージ コレクションの前にリソースを解放する手段を提供できます。 そのインターフェイスを実装するクラスでは、貴重なリソースを直ちに解放するために呼び出すことができる `Dispose` メソッドが公開されています。

`Using` ステートメントによって、リソースの取得、一連のステートメントの実行、さらにリソースの破棄のプロセスが自動化されます。 ただし、リソースで <xref:System.IDisposable> インターフェイスを実装する必要があります。 詳細については、「[Using ステートメント](using-statement.md)」を参照してください。

## <a name="example"></a>例

次の例では、各種オプションで `Dim` ステートメントを使用して変数を宣言しています。

[!code-vb[VbVbalrStatements#141](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class11.vb#141)]

## <a name="example"></a>例

次の例では、1 から 30 までの素数を一覧表示しています。 ローカル変数のスコープについては、コード コメントに説明しています。

[!code-vb[VbVbalrStatements#142](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class11.vb#142)]

## <a name="example"></a>例

次の例では、`speedValue` 変数がクラス レベルで宣言されています。 `Private` キーワードを使用して、変数を宣言しています。 変数には、`Car` クラスの任意のプロシージャからアクセスできます。

[!code-vb[VbVbalrStatements#144](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class11.vb#144)]

[!code-vb[VbVbalrStatements#145](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class11.vb#145)]

## <a name="see-also"></a>関連項目

- [Const ステートメント](const-statement.md)
- [ReDim ステートメント](redim-statement.md)
- [Option Explicit ステートメント](option-explicit-statement.md)
- [Option Infer ステートメント](option-infer-statement.md)
- [Option Strict ステートメント](option-strict-statement.md)
- [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
- [変数宣言](../../programming-guide/language-features/variables/variable-declaration.md)
- [配列](../../programming-guide/language-features/arrays/index.md)
- [オブジェクト初期化子: 名前付きの型と匿名型](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [匿名型](../../programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [オブジェクト初期化子: 名前付きの型と匿名型](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [方法: オブジェクト初期化子を使用してオブジェクトを宣言する](../../programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
- [ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)
