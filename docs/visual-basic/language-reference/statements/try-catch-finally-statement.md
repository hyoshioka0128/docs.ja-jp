---
title: Try...Catch...Finally ステートメント
description: Visual Basic の Try/Catch/Finally ステートメントで例外処理を使用する方法について説明します。
ms.date: 12/07/2018
f1_keywords:
- vb.Try...Catch...Finally
- vb.when
- vb.Finally
- vb.Catch
- vb.Try
helpviewer_keywords:
- Try...Catch...Finally statements
- Try statement [Visual Basic]
- try-catch exception handling, Try...Catch...Finally statements
- error handling, while running code
- Try statement [Visual Basic], Try...Catch...Finally
- Finally keyword [Visual Basic], Try...Catch...Finally
- Catch statement [Visual Basic]
- When keyword [Visual Basic]
- Visual Basic code, handling errors while running
- structured exception handling, Try...Catch...Finally statements
ms.assetid: d6488026-ccb3-42b8-a810-0d97b9d6472b
ms.openlocfilehash: 22f1611786a3da512632b5b547b7ef141c8f65c6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84391769"
---
# <a name="trycatchfinally-statement-visual-basic"></a>Try...Catch...Finally ステートメント (Visual Basic)

コード内の所定のブロックで発生する可能性のあるエラーの一部またはすべてに対して、コードを実行しながらエラー処理を実行できます。

## <a name="syntax"></a>構文

```vb
Try
    [ tryStatements ]
    [ Exit Try ]
[ Catch [ exception [ As type ] ] [ When expression ]
    [ catchStatements ]
    [ Exit Try ] ]
[ Catch ... ]
[ Finally
    [ finallyStatements ] ]
End Try
```

## <a name="parts"></a>指定項目

|用語|定義|
|---|---|
|`tryStatements`|任意。 エラーが発生する可能性のあるステートメント。 複合ステートメントにすることもできます。|
|`Catch`|任意。 複数の `Catch` ブロックが許可されています。 `Try` ブロックの処理中に例外が発生した場合、各 `Catch` ステートメントは、スローされた例外を表す `exception` を使用して、例外を処理するかどうかを判断するためにテキスト順に検証されます。|
|`exception`|任意。 任意の変数名を指定します。 `exception` の初期値は、スローされたエラーの値です。 キャッチされたエラーを指定するために `Catch` と共に使用します。 省略した場合は、`Catch` ステートメントが例外をキャッチします。|
|`type`|任意。 クラス フィルターの型を指定します。 `exception` の値が、`type` によって指定された型の値、または派生型の値の場合、識別子は例外オブジェクトにバインドされます。|
|`When`|任意。 `When` 句を含む `Catch` ステートメントは、`expression` が `True` に評価される場合にのみ例外をキャッチします。 `When` 句は、例外の型をチェックした後にのみ適用され、`expression` は例外を表す識別子を参照する場合があります。|
|`expression`|任意。 暗黙的に `Boolean` に変換される必要があります。 汎用フィルターを記述する任意の式。 通常、エラー番号でフィルター処理するために使用されます。 `When` キーワードと共に使用して、エラーがキャッチされる状況を指定します。|
|`catchStatements`|任意。 関連付けられた `Try` ブロックで発生するエラーを処理するステートメント。 複合ステートメントにすることもできます。|
|`Exit Try`|任意。 `Try...Catch...Finally` 構造体から抜け出すキーワード。 実行は、`End Try` ステートメントの直後のコードで再開されます。 `Finally` ステートメントは引き続き実行されます。 `Finally` ブロックでは許可されていません。|
|`Finally`|任意。 `Finally` ブロックは、実行が `Try...Catch` ステートメントの任意の部分から離れたときに常に実行されます。|
|`finallyStatements`|任意。 他のエラー処理がすべて実行された後で実行されるステートメント。|
|`End Try`|`Try...Catch...Finally` 構造体を終了します。|

## <a name="remarks"></a>Remarks

特定の例外がコードの特定のセクションで発生することが予想される場合は、コードを `Try` ブロックに配置し、`Catch` ブロックを使用して制御を維持し、例外が発生した場合は処理します。

`Try…Catch` ステートメントは、`Try` ブロックと、それに続く 1 つ以上の `Catch` 句で構成されます。この句にはさまざまな例外のハンドラーを指定します。 `Try` ブロックで例外がスローされると、Visual Basic では、この例外を処理する `Catch` ステートメントが検索されます。 一致する `Catch` ステートメントが見つからない場合、Visual Basic は、現在のメソッドを呼び出したメソッドを調べ、呼び出し履歴を調べていきます。 `Catch` ブロックが見つからない場合、Visual Basic は、ハンドルされない例外のメッセージをユーザーに表示し、プログラムの実行を停止します。

`Try…Catch` ステートメント内で複数の `Catch` ステートメントを使用できます。 これを実行すると、`Catch` 句は順序どおりにチェックされるため、順序が重要になります。 例外は、特殊性の高い順にキャッチしてください。

次の `Catch` ステートメントの条件は最も限定的ではなく、<xref:System.Exception> クラスから派生したすべての例外をキャッチします。 通常は、予期したすべての具体的な例外をキャッチした後、これらのバリエーションのいずれかを `Try...Catch...Finally` 構造体の最後の `Catch` ブロックとして使用してください。 制御フローは、次のいずれかのバリエーションに従う `Catch` ブロックに達することはできません。

- `type` が `Exception` である (例: `Catch ex As Exception`)

- ステートメントに `exception` 変数がない (例: `Catch`)

`Try…Catch…Finally` ステートメントが別の `Try` ブロック内に入れ子になっている場合、Visual Basic はまず、最も内側の `Try` ブロック内の各 `Catch` ステートメントを調べます。 一致する `Catch` ステートメントが見つからない場合、検索は外側の `Try…Catch…Finally` ブロックの `Catch` ステートメントに進みます。

`Try` ブロックのローカル変数は、個別のブロックであるため、`Catch` ブロックでは使用できません。 複数のブロックで変数を使用する場合は、`Try...Catch...Finally` 構造体の外側で変数を宣言します。

> [!TIP]
> `Try…Catch…Finally` ステートメントは、IntelliSense コード スニペットとして利用できます。 コード スニペット マネージャーで、 **[コード パターン - If、For Each、Try Catch、Property、その他]** を展開してから、 **[エラー処理 (例外)]** を展開します。 詳細については、「[Code Snippets](/visualstudio/ide/code-snippets)」を参照してください。

## <a name="finally-block"></a>Finally ブロック

`Try` 構造体を終了する前に実行する必要のあるステートメントが 1 つ以上ある場合は、`Finally` ブロックを使用します。 制御は、`Try…Catch` 構造体から渡される直前に `Finally` ブロックに渡されます。 これは、`Try` 構造体の内部のどこかで例外が発生した場合でも当てはまります。

`Finally` ブロックは、例外が発生した場合でも実行する必要があるコードを実行する場合に便利です。 制御は、`Try...Catch` ブロックの終了方法に関係なく、`Finally` ブロックに渡されます。

`Finally` ブロック内のコードは、コードが `Try` または `Catch` ブロックで `Return` ステートメントを検出した場合でも実行されます。 次の場合、制御は、`Try` または `Catch` ブロックから対応する `Finally` ブロックに渡されません。

- `Try` または `Catch` ブロックで [End ステートメント](end-statement.md)が検出された。

- `Try` または `Catch` ブロックで <xref:System.StackOverflowException> がスローされた。

実行を明示的に `Finally` ブロックに移動することは有効ではありません。 例外を除き、`Finally` ブロックからの実行を移動することは有効ではありません。

`Try` ステートメントに少なくとも 1 つの `Catch` ブロックが含まれていない場合は、`Finally` ブロックが含まれている必要があります。

> [!TIP]
> 特定の例外をキャッチする必要がない場合、`Using` ステートメントは、ブロックを終了する方法に関係なく、`Try…Finally` ブロックのように動作し、リソースの破棄を保証します。 これは、ハンドルされない例外が発生した場合でも当てはまります。 詳細については、「[Using ステートメント](using-statement.md)」を参照してください。

## <a name="exception-argument"></a>Exception 引数

`Catch` ブロックの `exception` 引数は、<xref:System.Exception> クラスのインスタンス、または `Exception` クラスから派生したクラスです。 `Exception` クラス インスタンスは、`Try` ブロックで発生したエラーに対応します。

`Exception` オブジェクトのプロパティは、例外の原因と場所を特定するのに役立ちます。 たとえば、<xref:System.Exception.StackTrace%2A> プロパティは、例外の原因となった呼び出し元のメソッドを一覧表示し、コード内でエラーが発生した場所を見つけるのに役立ちます。 <xref:System.Exception.Message%2A> は、例外について説明するメッセージを返します。 <xref:System.Exception.HelpLink%2A> は、関連付けられたヘルプ ファイルへのリンクを返します。 <xref:System.Exception.InnerException%2A> は、現在の例外の原因となった `Exception` オブジェクトを返します。元の `Exception` がない場合は `Nothing` を返します。

## <a name="considerations-when-using-a-trycatch-statement"></a>Try…Catch ステートメントを使用する場合の考慮事項

`Try…Catch` ステートメントは、異常な、または予期しないプログラム イベントの発生を通知するためにのみ使用します。 これには、次のような理由があります。

- 実行時に例外をキャッチするとオーバーヘッドが増加するため、例外を回避するための事前チェックよりも低速になる可能性がある。

- `Catch` ブロックが正しく処理されない場合は、例外がユーザーに正しく報告されない可能性がある。

- 例外処理により、プログラムがより複雑になる。

発生する可能性がある条件をチェックするために、必ずしも `Try…Catch` ステートメントは必要ありません。 次の例では、ファイルを開こうとする前に、そのファイルが存在するかどうかを確認します。 これにより、<xref:System.IO.File.OpenText%2A> メソッドによってスローされた例外をキャッチする必要がなくなります。

[!code-vb[VbVbalrStatements#94](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#94)]

スレッドセーフなログ記録と適切なメッセージのどちらを使用しても、`Catch` ブロック内のコードでユーザーに例外を適切に報告できることを確認します。 そうでない場合、例外は不明なままになる可能性があります。

## <a name="async-methods"></a>非同期メソッド

メソッドに [Async](../modifiers/async.md) 修飾子を付けると、そのメソッドで [Await](../operators/await-operator.md) 演算子を使用できます。 `Await` 演算子を含むステートメントは、待機しているタスクが完了するまでメソッドの実行を中断します。 このタスクは、進行中の作業を表します。 `Await` 演算子に関連付けられているタスクが終了すると、実行は同じメソッド内で再開されます。 詳細については、「[非同期プログラムにおける制御フロー](../../programming-guide/concepts/async/control-flow-in-async-programs.md)」を参照してください。

非同期メソッドによって返されるタスクは、ハンドルされない例外が原因で完了したことを示す違反状態で終了することがあります。 また、タスクは取り消された状態で終了することもあります。その結果、await 式から `OperationCanceledException` がスローされます。 いずれかの種類の例外をキャッチするには、タスクに関連付けられている `Await` 式を `Try` ブロックに配置し、`Catch` ブロックで例外をキャッチします。 例については、このトピックで後述します。

複数の例外が違反の原因になっているため、タスクが違反状態になることがあります。 たとえば、タスクは <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> の呼び出しの結果になることがあります。 このようなタスクを待機した場合、キャッチされた例外は例外の 1 つにすぎず、どの例外がキャッチされるかは予測できません。 例については、このトピックで後述します。

`Await` 式を `Catch` ブロックや `Finally` ブロックに記述することはできません。

## <a name="iterators"></a>Iterators

iterator 関数または `Get` アクセサーは、コレクションに対するカスタムの反復を実行します。 反復子は、[Yield](yield-statement.md) ステートメントを使用して、コレクションの各要素を 1 回に 1 つ返します。 [For Each...Next ステートメント](for-each-next-statement.md)を使用して、iterator 関数を呼び出します。

`Yield` ステートメントは `Try` ブロック内に記述できます。 `Yield` ステートメントが含まれている `Try` ブロックには、`Catch` ブロックと `Finally` ブロックを記述することができます。 例については、「[反復子](../../programming-guide/concepts/iterators.md)」の「Visual Basic の Try ブロック」セクションを参照してください。

`Yield` ステートメントを `Catch` ブロックや `Finally` ブロックに記述することはできません。

(iterator 関数の外部の) `For Each` 本体で例外がスローされた場合、iterator 関数の `Catch` ブロックは実行されず、iterator 関数の `Finally` ブロックが実行されます。 iterator 関数内の `Catch` ブロックでキャッチされるのは、iterator 関数内で発生した例外だけです。

## <a name="partial-trust-situations"></a>部分信頼の状況

部分信頼の状況 (ネットワーク共有でホストされているアプリケーションなど) では、`Try...Catch...Finally` は、呼び出しを含むメソッドが呼び出される前に発生したセキュリティ例外をキャッチしません。 次の例では、サーバー共有に配置し、そこから実行すると、エラー "System.Security.SecurityException:要求が失敗しました。" が生成されます。 セキュリティ例外の詳細については、<xref:System.Security.SecurityException> クラスを参照してください。

[!code-vb[VbVbalrStatements#85](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#85)]

このような部分信頼では、`Process.Start` ステートメントを別の `Sub` に配置する必要があります。 `Sub` の最初の呼び出しは失敗します。 これにより、`Process.Start` を含む `Sub` が開始されてセキュリティ例外が生成される前に、`Try...Catch` をキャッチできます。

## <a name="examples"></a>使用例

### <a name="the-structure-of-trycatchfinally"></a>Try...Catch...Finally の構造

次の例は、`Try...Catch...Finally` ステートメントの構造を示しています。

[!code-vb[VbVbalrStatements#86](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#86)]  

### <a name="exception-in-a-method-called-from-a-try-block"></a>Try ブロックから呼び出されたメソッドでの例外

次の例では、`CreateException` メソッドは `NullReferenceException` をスローします。 例外を生成するコードが `Try` ブロックに含まれていません。 したがって、`CreateException` メソッドは例外を処理しません。 `RunSample` メソッドは、`CreateException` メソッドの呼び出しが `Try` ブロック内にあるため、例外を処理します。

この例には、いくつかの種類の例外の `Catch` ステートメントが含まれており、最も具体的なものから順に示されています。

[!code-vb[VbVbalrStatements#91](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#91)]

### <a name="the-catch-when-statement"></a>Catch When ステートメント

次の例では、`Catch When` ステートメントを使用して条件式をフィルター処理する方法を示します。 条件式が `True` と評価された場合、`Catch` ブロック内のコードが実行されます。

[!code-vb[VbVbalrStatements#92](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#92)]

### <a name="nested-try-statements"></a>入れ子になった Try ステートメント

次の例では、`Try` ブロックに含まれる `Try…Catch` ステートメントが含まれます。 内側の `Catch` ブロックは、その `InnerException` プロパティが元の例外に設定されている例外をスローします。 外側の `Catch` ブロックは、独自の例外と内部例外を報告します。

[!code-vb[VbVbalrStatements#93](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#93)]

### <a name="exception-handling-for-async-methods"></a>非同期メソッドの例外処理

次の例では、非同期メソッドの例外処理を示します。 非同期タスクに適用される例外をキャッチするために、`Await` 式は呼び出し元の `Try` ブロックにあり、例外は `Catch` ブロックでキャッチされます。

例外処理を示すために、この例の `Throw New Exception` 行のコメントを解除します。 例外が `Catch` ブロックでキャッチされ、タスクの `IsFaulted` プロパティが `True` に設定され、タスクの `Exception.InnerException` プロパティが例外に設定されます。

`Throw New OperationCancelledException` 行のコメントを解除して、非同期処理を取り消したときに何が起こるかを示します。 例外が `True` ブロックでキャッチされ、タスクの `Catch` プロパティが `IsCanceled` に設定されます。 ただし、この例に該当しない一部の条件では、`IsFaulted` が `True` に設定され、`IsCanceled` が `False` に設定されます。

[!code-vb[csAsyncExceptions#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncexceptions/vb/class1.vb#1)]

### <a name="handling-multiple-exceptions-in-async-methods"></a>非同期メソッドの複数の例外の処理

次の例では、複数のタスクで複数の例外が発生する可能性がある例外処理について説明します。 `Try` ブロックには、<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> で返されたタスクの `Await` 式が含まれています。 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> が適用される 3 つのタスクが完了すると、このタスクは完了します。

3 つのタスクでそれぞれ例外が発生します。 `Catch` ブロックは例外を反復処理します。この例外は、`Task.WhenAll` が返したタスクの `Exception.InnerExceptions` プロパティで見つかります。

[!code-vb[csAsyncExceptions#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncexceptions/vb/class1.vb#3)]

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:System.Exception>
- [Exit ステートメント](exit-statement.md)
- [On Error ステートメント](on-error-statement.md)
- [コード スニペットを使用するためのベスト プラクティス](/visualstudio/ide/best-practices-for-using-code-snippets)
- [例外処理](../../../standard/parallel-programming/exception-handling-task-parallel-library.md)
- [Throw ステートメント](throw-statement.md)
