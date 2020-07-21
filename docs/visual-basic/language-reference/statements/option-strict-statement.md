---
title: Option Strict Statement
ms.date: 07/20/2015
f1_keywords:
- vb.Strict
- vb.OptionStrict
helpviewer_keywords:
- Strict keyword [Visual Basic]
- Option Strict statement [Visual Basic]
- conversions [Visual Basic], implicit
- late binding [Visual Basic]
- implicit conversions [Visual Basic]
ms.assetid: 5883e0c1-a920-4274-8e46-b0ff047eaee5
ms.openlocfilehash: 9c86ae6be86591445dde3cc4e7bdd38aa4a7f0fa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404344"
---
# <a name="option-strict-statement"></a>Option Strict Statement
暗黙的なデータ型変換を拡大変換のみに制限し、遅延バインディングを許可せず、`Object` 型になる暗黙的な型指定も許可しません。  
  
## <a name="syntax"></a>構文  
  
```vb  
Option Strict { On | Off }  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`On`|任意。 `Option Strict` チェックを有効にします。|  
|`Off`|任意。 `Option Strict` チェックを無効にします。|  
  
## <a name="remarks"></a>Remarks  
 `Option Strict On` または `Option Strict` がファイルに存在すると、次の条件によりコンパイル時エラーが発生します。  
  
- 暗黙的な縮小変換  
  
- 遅延バインディング  
  
- 結果が `Object` 型となる暗黙の型指定  
  
> [!NOTE]
> [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) で設定できる警告の構成には、コンパイル時エラーが発生する 3 つの条件に相当する 3 つの設定があります。 これらの設定の使用方法については、このトピックで後述する「[IDE で警告の構成を設定するには](option-strict-statement.md#conditions)」を参照してください。  
  
 関連付けられている IDE 設定でこれらのエラーまたは警告をオンにするように指定している場合でも、`Option Strict Off` ステートメントは、3 つの条件すべてについてエラーおよび警告チェックをオフにします。 `Option Strict On` ステートメントは、関連する IDE 設定でこれらのエラーまたは警告をオフにするように指定している場合でも、3 つの条件すべてについてエラーおよび警告チェックをオンにします。  
  
 使用する場合、`Option Strict` ステートメントは、ファイル内のどのソース ステートメントよりも前に記述する必要があります。  
  
 `Option Strict` を `On` に設定すると、Visual Basic では、すべてのプログラミング要素にデータ型が指定されているかどうかがチェックされます。 データ型は、明示的に指定することも、ローカル型推論を使用して指定することもできます。 次の理由から、すべてのプログラミング要素にデータ型を指定することをお勧めします。  
  
- これにより、変数とパラメーターの IntelliSense サポートが有効になります。 これにより、コードを入力しながら、プロパティとその他のメンバーを確認できます。  
  
- これにより、コンパイラは型チェックを実行できます。 型チェックを使用すると、型変換エラーのために実行時に失敗する可能性があるステートメントを見つけることができます。 また、これらのメソッドをサポートしていないオブジェクトに対するメソッドの呼び出しも識別します。  
  
- これにより、コードの実行速度が向上します。 その理由の 1 つは、プログラミング要素のデータ型を指定しない場合、Visual Basic コンパイラによって `Object` 型に割り当てられることです。 コンパイルされたコードは、`Object` とその他のデータ型との間で変換を行う必要があり、これによりパフォーマンスが低下します。  
  
## <a name="implicit-narrowing-conversion-errors"></a>暗黙的な縮小変換エラー  
 縮小変換する暗黙的なデータ型変換がある場合は、暗黙的な縮小変換エラーが発生します。  
  
 Visual Basic は、さまざまなデータ型を他のデータ型に変換できます。 あるデータ型の値を精度が低いデータ型または容量の小さいデータ型に変換すると、データ損失が発生する可能性があります。 このような縮小変換が失敗すると、実行時エラーが発生します。 `Option Strict` を使用すると、このような縮小変換についてコンパイル時に通知が送信されるため、変換を回避できます。 詳細については、「[暗黙の型変換と明示的な型変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)」および「[拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)」を参照してください。  
  
 エラーを発生させる可能性のある変換には、式で発生する暗黙的な変換が含まれます。 詳細については、次のトピックを参照してください。  
  
- [+ 演算子](../operators/addition-operator.md)  
  
- [+= 演算子](../operators/addition-assignment-operator.md)  
  
- [\ 演算子 (Visual Basic)](../operators/integer-division-operator.md)  
  
- [/= 演算子 (Visual Basic)](../operators/floating-point-division-assignment-operator.md)  
  
- [Char データ型](../data-types/char-data-type.md)  
  
 [& 演算子](../operators/concatenation-operator.md)を使用して文字列を連結する場合、文字列へのすべての変換は拡大と見なされます。 したがって、`Option Strict` がオンの場合でも、これらの変換では暗黙的な縮小変換エラーは生成されません。  
  
 対応するパラメーターとは異なるデータ型の引数を持つメソッドを呼び出すと、`Option Strict` がオンになっている場合は、縮小変換によってコンパイル時エラーが発生します。 拡大変換または明示的な変換を使用すると、コンパイル時エラーを回避できます。  
  
 `For Each…Next` コレクション内の要素からループ制御変数への変換では、コンパイル時に暗黙的な縮小変換エラーが抑制されます。 これは、`Option Strict` がオンになっている場合でも発生します。 詳細については、「[For Each...Next ステートメント](for-each-next-statement.md)」の縮小変換に関するセクションを参照してください。  
  
## <a name="late-binding-errors"></a>遅延バインディング エラー  
 `Object` 型として宣言された変数のプロパティまたはメソッドにオブジェクトを代入する場合は、そのオブジェクトは遅延バインディングされます。 詳細については、「[事前バインディングと遅延バインディング](../../programming-guide/language-features/early-late-binding/index.md)」を参照してください。  
  
## <a name="implicit-object-type-errors"></a>暗黙的なオブジェクトの型エラー  
 適切な型が宣言された変数を推論できない場合は暗黙的なオブジェクトの型エラーが発生するため、`Object` の型が推論されます。 これは主に、`As` 句を使用せず、`Option Infer` をオフにして、`Dim` ステートメントを使用して変数を宣言した場合に発生します。 詳細については、「[Option Infer ステートメント](option-infer-statement.md)」および「[Visual Basic 言語仕様](../../reference/language-specification/index.md)」を参照してください。  
  
 メソッドのパラメーターで `Option Strict` がオフの場合、`As` 句は省略可能です。 ただし、いずれかのパラメーターが `As` 句を使用する場合は、すべてで使用する必要があります。 `Option Strict` がオンの場合は、すべてのパラメーター定義に対して `As` 句が必要です。  
  
 `As` 句を使用せずに変数を宣言し、それを `Nothing` に設定すると、変数の型は `Object` になります。 この場合、`Option Strict` がオンで `Option Infer` がオンの場合、コンパイル時エラーは発生しません。 この例が `Dim something = Nothing` です。  
  
### <a name="default-data-types-and-values"></a>既定のデータ型と値  
 次の表では、[Dim ステートメント](dim-statement.md)のデータ型と初期化子を指定するさまざまな組み合わせの結果を示します。  
  
|データ型が指定されているか|初期化子が指定されているか|例|結果|  
|---|---|---|---|  
|いいえ|いいえ|`Dim qty`|`Option Strict` がオフ (既定値) の場合、変数は `Nothing` に設定されます。<br /><br /> `Option Strict` がオンの場合、コンパイル時エラーが発生します。|  
|いいえ|はい|`Dim qty = 5`|`Option Infer` がオン (既定値) の場合、変数は初期化子のデータ型になります。 「[ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)」を参照してください。<br /><br /> `Option Infer` がオフで、`Option Strict` がオフの場合、変数は `Object` のデータ型になります。<br /><br /> `Option Infer` がオフで、`Option Strict` がオンの場合、コンパイル時エラーが発生します。|  
|はい|いいえ|`Dim qty As Integer`|変数は、データ型の既定値に初期化されます。 詳細については、「[Dim ステートメント](dim-statement.md)」を参照してください。|  
|はい|はい|`Dim qty  As Integer = 5`|初期化子のデータ型を指定したデータ型に変換できない場合は、コンパイル時エラーが発生します。|  
  
## <a name="when-an-option-strict-statement-is-not-present"></a>Option Strict ステートメントが指定されていない場合  
 ソース コードに `Option Strict` ステートメントが含まれていない場合は、[[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) の **[Option strict]** 設定が使用されます。 **[コンパイル] ページ**には、エラーを生成する条件をさらに制御するための設定があります。  
  
 コマンドライン コンパイラを使用している場合は、[-optionstrict](../../reference/command-line-compiler/optionstrict.md) コンパイラ オプションを使用して `Option Strict` の設定を指定できます。  
  
### <a name="to-set-option-strict-in-the-ide"></a>IDE の Option Strict を設定するには  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[コンパイル]** タブで、 **[Option Strict]** ボックスの値を設定します。  
  
### <a name="to-set-warning-configurations-in-the-ide"></a><a name="conditions"></a> IDE で警告の構成を設定するには  
 `Option Strict` ステートメントの代わりに [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) を使用している場合は、エラーを生成する条件をさらに制御できます。 **[コンパイル]** ページの **[警告の構成]** セクションには、`Option Strict` がオンになっているときにコンパイル時エラーが発生する 3 つの条件に相当する設定があります。 これらの設定を次に示します。  
  
- **暗黙的な変換**  
  
- **遅延バインディング、呼び出しが実行時に失敗する可能性があります**  
  
- **暗黙的な型、オブジェクトと見なされます**  
  
 **[Option Strict]** を **[オン]** に設定すると、これら 3 つの警告の構成設定のすべてが **[エラー]** に設定されます。 **[Option Strict]** を **[オフ]** に設定すると、3 つの設定すべてが **[なし]** に設定されます。  
  
 各警告の構成設定を個別に **[なし]** 、 **[警告]** 、または **[エラー]** に変更することができます。 3 つの警告の構成設定がすべて **[エラー]** に設定されている場合、`Option strict` ボックスに `On` が表示されます。 3 つすべてが **[なし]** に設定されている場合、このボックスには `Off` が表示されます。 これらの設定のその他の組み合わせに対しては、 **(カスタム)** が表示されます。  
  
### <a name="to-set-the-option-strict-default-setting-for-new-projects"></a>新しいプロジェクトの Option Strict の既定の設定を設定するには  
 プロジェクトを作成するときに、 **[コンパイル]** タブの **[Option Strict]** 設定が **[オプション]** ダイアログ ボックスの **[Option Strict]** 設定に設定されます。  
  
 このダイアログ ボックスの `Option Strict` を設定するには、 **[ツール]** メニューの **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスの **[プロジェクトおよびソリューション]** を展開し、 **[VISUAL BASIC の既定値]** をクリックします。 **[VISUAL BASIC の既定値]** の初期の既定値は `Off` です。  
  
### <a name="to-set-option-strict-on-the-command-line"></a>コマンド ラインで Option Strict を設定するには  
 **vbc** コマンドに [-optionstrict](../../reference/command-line-compiler/optionstrict.md) コンパイラ オプションを含めます。  
  
## <a name="example"></a>例  
 次の例は、縮小変換である暗黙の型変換によって発生するコンパイル時のエラーを示しています。 このカテゴリのエラーは、 **[コンパイル] ページ**の **[暗黙的な変換]** 条件に対応しています。  
  
 [!code-vb[VbVbalrStatements#161](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#161)]  
  
## <a name="example"></a>例  
 次の例は、遅延バインディングによって発生したコンパイル時エラーを示しています。 このカテゴリのエラーは、 **[コンパイル] ページ**の **[遅延バインディングです。呼び出しが実行時に失敗する可能性があります]** 条件に対応しています。  
  
 [!code-vb[VbVbalrStatements#162](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#162)]  
  
## <a name="example"></a>例  
 次の例は、暗黙的な型の `Object` で宣言された変数によって発生するエラーを示しています。 このカテゴリのエラーは **[コンパイル] ページ**の **[暗黙的な型です。オブジェクトと見なされます]** 条件に対応しています。  
  
 [!code-vb[VbVbalrStatements#163](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#163)]  
  
 [!code-vb[VbVbalrStatements#164](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#164)]  
  
## <a name="see-also"></a>関連項目

- [拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [暗黙の型変換と明示的な型変換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
- [Option Explicit ステートメント](option-explicit-statement.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [方法: オブジェクトのメンバーにアクセスする](../../programming-guide/language-features/variables/how-to-access-members-of-an-object.md)
- [XML での埋め込み式](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md)
- [厳密でないデリゲート変換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [Office ソリューションの遅延バインディング](/visualstudio/vsto/late-binding-in-office-solutions)
- [-optionstrict](../../reference/command-line-compiler/optionstrict.md)
- [[Visual Basic の既定値] ([オプション] ダイアログ ボックス - [プロジェクト])](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
