---
title: タプル
ms.date: 04/23/2017
helpviewer_keywords:
- tuples [Visual Basic]
ms.assetid: 3e66cd1b-3432-4e1d-8c37-5ebacae8f53f
ms.openlocfilehash: 378ee4e7d3a3b106b719e5da819b09f336ff218e
ms.sourcegitcommit: 67cf756b033c6173a1bbd1cbd5aef1fccac99e34
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86226661"
---
# <a name="tuples-visual-basic"></a>タプル (Visual Basic)

Visual Basic 2017 以降、Visual Basic 言語ではタプルの組み込みサポートが提供されています。これによって、タプルの作成とタプルの要素へのアクセスが簡単になります。 タプルは、特定の数とシーケンスの値が含まれる軽量なデータ構造です。 タプルをインスタンス化するときは、各値 (または要素) の数とデータ型を定義します。 たとえば、2 タプル (つまりペア) には 2 つの要素があります。 1 つ目を `Boolean` 値、2つ目を `String` にすることができます。 タプルを使用すると複数の値を 1 つのオブジェクトに簡単に格納できるので、多くの場合、メソッドから複数の値を返すための軽量な方法として使用されます。

> [!IMPORTANT]
> タプルのサポートには <xref:System.ValueTuple> 型が必要です。 .NET Framework 4.7 がインストールされていない場合は、NuGet ギャラリーから入手できる NuGet パッケージ `System.ValueTuple` を追加する必要があります。 このパッケージがないと、"定義済みの型 'ValueTuple(Of,,,)' は定義またはインポートされていません" のようなコンパイル エラーが発生することがあります。

## <a name="instantiating-and-using-a-tuple"></a>タプルのインスタンス化と使用

タプルをインスタンス化するには、コンマ区切り値をかっこで囲みます。 これらの値のそれぞれがタプルのフィールドになります。 たとえば、次のコードではトリプル (つまり 3 タプル) が定義されており、`Date` が 1 つ目の値、`String` が 2 つ目の値、`Boolean` が 3 つ目の値です。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#1)]

既定では、タプルの各フィールドの名前は、文字列 `Item` と、タプル内のフィールドの位置を示す 1 から始まる数字で構成されます。 この 3 タプルでは、`Date` フィールドが `Item1`、`String` フィールドが `Item2`、`Boolean` フィールドが `Item3` です。 次の例では、前のコード行でインスタンス化されたタプルのフィールドの値を表示します。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#2)]

Visual Basic タプルのフィールドは読み取り/書き込み可能です。タプルをインスタンス化すると、その値を変更できます。 次の例では、前の例で作成したタプルの 3 つのフィールドのうち 2 つを変更し、結果を表示します。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#3)]

## <a name="instantiating-and-using-a-named-tuple"></a>名前付きタプルのインスタンス化と使用

タプルのフィールドに既定の名前を使用するのではなく、独自の名前をタプルの要素に割り当てることによって、"*名前付きタプル*" をインスタンス化できます。 その後、タプルのフィールドに、割り当てられた名前 "*または*" 既定の名前でアクセスできます。 次の例では、前と同じ 3 タプルをインスタンス化していますが、1 つ目のフィールド `EventDate`、2 つ目 `Name`、3 つ目 `IsHoliday` を明示的に指定する点が異なります。 次に、フィールド値を表示し、変更してから、フィールドの値を再度表示します。

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#4)]

## <a name="inferred-tuple-element-names"></a>推論されたタプル要素の名前

Visual Basic 15.3 以降では、Visual Basic がタプル要素の名前を推定できます。明示的に割り当てる必要はありません。 推定タプル名は、一連の変数からタプルを初期化するときに、タプル要素名を変数名と同じにする場合に便利です。

次の例では、明示的に指定された3つの要素、`state`、`stateName`、および `capital` を含む `stateInfo` タプルを作成します。 要素の名前を付けるとき、タプルの初期化ステートメントにより、名前が付けられる要素に同じ名前の変数の値が単に代入されることに注意してください。

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#1)]

要素と変数の名前が同じであるため、次の例に示すように、Visual Basic コンパイラがフィールドの名前を推定できます。

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#2)]

推定タプル要素名を有効にするには、Visual Basic プロジェクト (\*.vbproj) ファイルに使用する Visual Basic コンパイラのバージョンを定義する必要があります。

```xml
<PropertyGroup>
  <LangVersion>15.3</LangVersion>
</PropertyGroup>
```

バージョン番号として、15.3 以降の任意の Visual Basic コンパイラ バージョンを指定できます。 特定のコンパイラ バージョンをハードコーディングする代わりに、`LangVersion` の値として "Latest" を指定すると、システムにインストールされている最新バージョンの Visual Basic コンパイラでコンパイルすることもできます。

詳細については、[Visual Basic 言語バージョンの設定](../../../language-reference/configure-language-version.md)に関するページを参照してください。

場合によっては、Visual Basic コンパイラが候補名からタプル要素名を推定できないことがあり、`Item1`、`Item2` などの既定名を使用しないとタプル フィールドを参照できません。次の設定があります。

- 候補名が、タプル メンバーの名前と同じです (`Item3`、`Rest`、`ToString` など)。

- 候補名がタプル内で重複しています。

フィールド名の推定に失敗しても、Visual Basic はコンパイラ エラーを生成せず、実行時に例外がスローされることもありません。 代わりに、`Item1` や `Item2` など、定義済みの名前でタプル フィールドを参照する必要があります。

## <a name="tuples-versus-structures"></a>タプルと構造体

Visual Basic のタプルは、**System.ValueTuple** ジェネリック型の 1 つのインスタンスである値型です。 たとえば、前の例で定義されている `holiday` タプルは、<xref:System.ValueTuple%603> 構造体のインスタンスです。 これは、データの軽量コンテナーとして設計されています。 タプルは、複数のデータ項目を含むオブジェクトを簡単に作成することを目的としているため、カスタム構造体であれば備えている機能の一部が欠落しています。 次の設定があります。

- カスタム メンバー。 タプルに対して独自のプロパティ、メソッド、またはイベントを定義することはできません。

- 検証。 フィールドに代入されたデータを検証することはできません。

- 不変性。 Visual Basic のタプルは変更可能です。 対照的に、カスタム構造体では、インスタンスを変更可能にするかどうかを制御できます。

カスタム メンバー、プロパティとフィールドの検証、または不変性が重要な場合は、Visual Basic の [Structure](../../../language-reference/statements/structure-statement.md) ステートメントを使用してカスタム値型を定義する必要があります。

Visual Basic のタプルは、**ValueTuple** 型のメンバーを継承します。 フィールドに加えて、次のメソッドが含まれています。

| メンバー | 説明 |
| ---|---|
| CompareTo | 現在のタプルを、同じ数の要素を持つ別のタプルと比較します。 |
| 次の値に等しい | 現在のタプルが別のタプルまたはオブジェクトと等しいかどうかを判断します。 |
| GetHashCode | 現在のインスタンスのハッシュ コードを計算します。 |
| ToString | `(Item1, Item2...)` という形式で、このタプルの文字列表現を返します。`Item1` と `Item2` はタプルのフィールドの値を表しています。 |

さらに、**ValueTuple** 型は <xref:System.Collections.IStructuralComparable> および <xref:System.Collections.IStructuralEquatable> インターフェイスを実装し、これらによって顧客の比較機能を定義できます。

## <a name="assignment-and-tuples"></a>割り当てとタプル

Visual Basic では、同じ数のフィールドを含むタプル型の間の代入がサポートされます。 次のいずれかに該当する場合は、フィールドの型を変換できます。

- 代入元と代入先のフィールドの型が同じです。

- 代入元の型から代入先の型への拡大 (つまり暗黙) の変換が定義されています。

- `Option Strict` が `On` になっており、代入元の型から代入先の型への縮小 (つまり明示的) の変換が定義されています。 代入元の値が代入先の型の範囲外の場合、この変換によって例外がスローされる可能性があります。

他の変換は、割り当てでは考慮されません。 タプル型間で許可されている割り当ての種類を見てみましょう。

以降の例で使用されている変数について考えます。

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#1)]

最初の 2 つの変数 `unnamed` および `anonymous` では、フィールドにセマンティック名が割り当てられていません。 フィールド名は、既定の `Item1` と `Item2` です。 最後の 2 つの変数 `named` および `differentName` には、セマンティック フィールド名が付けられています。 この 2 つのタプルでは、フィールド名が異なっていることに注意してください。

この 4 つのタプルに含まれているフィールドの数 ("アリティ" と呼ばれます) とフィールドの型は同じです。 このため、これらの割り当てはすべて機能します。

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#2)]

タプルの名前が割り当てられていないことに注意してください。 フィールドの値は、タプルのフィールドの順序に従って割り当てられます。

最終的に、`named` の 1 つ目のフィールドが `Integer` で、`Long` の 1 つ目のフィールドが `conversion` でも、`named` タプルを `conversion` タプルに代入できることに注意してください。 この代入が成功するのは、`Integer` から `Long` への変換が拡大変換であるためです。

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#3)]

フィールドの数が異なるタプルは代入できません。

```vb
' Does not compile.
' VB30311: Value of type '(Integer, Integer, Integer)' cannot be converted
'          to '(Answer As Integer, Message As String)'
var differentShape = (1, 2, 3)
named = differentShape
```

## <a name="tuples-as-method-return-values"></a>メソッドの戻り値としてのタプル

1 つのメソッドで返すことができる値は 1 つのみです。 しかし、1 回のメソッド呼び出しで複数の値を返すことが望ましい場合がよくあります。 この制限を回避するには、いくつかの方法があります。

- カスタム クラスまたは構造体を作成して、そのプロパティまたはフィールドがメソッドによって返される値を表すようにできます。 これは、重量ソリューションです。メソッド呼び出しの値を取得するためだけにカスタム型を定義する必要があります。

- メソッドから 1 つの値を返し、メソッドの参照によって残りの値を渡して返すことができます。 これは、変数をインスタンス化する際のオーバーヘッドが発生し、参照によって渡す変数の値が誤って上書きされるリスクがあります。

- 複数の戻り値を取得するための軽量ソリューションを提供するタプルを使用できます。

たとえば、.NET の **TryParse** メソッドは、解析操作が成功したかどうかを示す `Boolean` 値を返します。 解析操作の結果は、メソッドへの参照によって渡される変数で返されます。 通常、<xref:System.Int32.TryParse%2A?displayProperty=nameWithType> などの解析メソッドを呼び出すと、次のようになります。

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#1)]

<xref:System.Int32.TryParse%2A?displayProperty=nameWithType> メソッドへの呼び出しを独自のメソッドでラップすると、解析操作からタプルを返すことができます。 次の例では、`NumericLibrary.ParseInteger` が <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> メソッドを呼び出し、2 つの要素を含む名前付きタプルを返します。

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

さらに、次のコードを使用してメソッドを呼び出すことができます。

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)]

## <a name="visual-basic-tuples-and-tuples-in-the-net-framework"></a>Visual Basic のタプルと .NET Framework のタプル

Visual Basic のタプルは、.NET Framework 4.7 に導入された **System.ValueTuple** ジェネリック型の 1 つのインスタンスです。 .NET Framework には、一連のジェネリック **System.Tuple** クラスも含まれています。 ただし、これらのクラスは、Visual Basic のタプルや **System.ValueTuple** ジェネリック型とはいくつかの点で異なっています。

- **Tuple** クラスの要素は、`Item1`、`Item2` などと名前が付けられるプロパティです。 Visual Basic のタプルと **ValueTuple** 型では、タプルの要素はフィールドです。

- **Tuple** インスタンスまたは **ValueTuple** インスタンスの要素には、わかりやすい名前を割り当てることはできません。 Visual Basic では、フィールドの意味を伝える名前を割り当てることができます。

- **Tuple** インスタンスのプロパティは読み取り専用です。つまり、タプルは変更不可能です。 Visual Basic のタプルと **ValueTuple** 型では、タプルのフィールドは読み取り/書き込み可能です。つまり、タプルは変更可能です。

- ジェネリック **Tuple** 型は参照型です。 これらの **Tuple** 型の使用は、オブジェクトの割り当てを意味します。 ホット パスでは、これがアプリケーションのパフォーマンスに大きな影響を及ぼすことがあります。 Visual Basic のタプルと **ValueTuple** 型は値型です。

<xref:System.TupleExtensions> クラスの拡張メソッドを使用すると、Visual Basic のタプルと .NET **Tuple** オブジェクトの変換が簡単になります。 **ToTuple** メソッドは Visual Basic のタプルを .NET **Tuple** オブジェクトに変換し、**ToValueTuple** メソッドは .NET **Tuple** オブジェクトを Visual Basic のタプルに変換します。

次の例では、タプルを作成し、それを .NET **Tuple** オブジェクトに変換してから、再び Visual Basic のタプルに変換しています。 例は、その後、このタプルと最初のタプルを比較して、等しいことを確認しています。

[!code-vb[Convert](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple2.vb#1)]

## <a name="see-also"></a>関連項目

- [Visual Basic の言語リファレンス](index.md)
