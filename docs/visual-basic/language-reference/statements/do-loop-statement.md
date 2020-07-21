---
title: Do...Loop ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Do
- vb.Loop
- vb.Until
helpviewer_keywords:
- conditional statements [Visual Basic], Do�Loop
- while statement [Visual Basic], Do...Loop
- execution [Visual Basic], conditional
- Do loops
- Until keyword [Visual Basic], Do...Loop statement
- Do...Loop statement
- instructions, repeating
- Do statement [Visual Basic]
- Exit statement [Visual Basic], in Do...Loop statements
- loop structures [Visual Basic], Do�Loop statements
- do-while statements [Visual Basic]
- loops, exiting
- Loop keyword [Visual Basic], Do...Loop statement
ms.assetid: 892f9096-b3e2-4aee-834d-83bc4e2c379d
ms.openlocfilehash: a9ec6caccbe161a39b592a642a938b81bae911a6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404785"
---
# <a name="doloop-statement-visual-basic"></a>Do...Loop ステートメント (Visual Basic)
`Boolean` 条件が `True` の場合、または条件が `True` になるまで、ステートメントのブロックを繰り返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Do { While | Until } condition  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop  
' -or-  
Do  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop { While | Until } condition  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`Do`|必須です。 `Do` ループの定義を開始します。|  
|`While`|`Until` を使用しない場合に、必ず指定します。 `condition` が `False` になるまでループを繰り返します。|  
|`Until`|`While` を使用しない場合に、必ず指定します。 `condition` が `True` になるまでループを繰り返します。|  
|`condition`|任意。 `Boolean` 式。 `condition` が `Nothing` の場合、Visual Basic はそれを `False` として扱います。|  
|`statements`|任意。 `condition` が `True` である間、またはその状態になるまで繰り返される、1 つまたは複数のステートメント。|  
|`Continue Do`|任意。 `Do` ループの次の反復に制御を渡します。|  
|`Exit Do`|任意。 `Do` ループから制御を移します。|  
|`Loop`|必須です。 `Do` ループの定義を終了します。|  
  
## <a name="remarks"></a>Remarks  
 条件が満たされるまで、一連のステートメントを無限に繰り返す場合は、`Do...Loop` 構造体を使用します。 ステートメントを設定した回数だけ繰り返す場合は、通常、[For...Next ステートメント](for-next-statement.md)のほうが適しています。  
  
 `While` または `Until` のいずれかを使用して `condition` を指定できますが、両方を指定することはできません。  
  
 `condition` は、ループの開始時または終了時に 1 回だけテストできます。 ループの開始時に (`Do` ステートメントで) `condition` をテストする場合、ループは 1 回も実行されない可能性があります。 ループの最後に (`Loop` ステートメントで) テストする場合、ループは少なくとも 1 回は必ず実行されます。  
  
 通常、条件は 2 つの値を比較することによって判断されますが、[ブール データ型](../data-types/boolean-data-type.md)の値 (`True` または `False`) に評価される任意の式を使用することもできます。 これには、`Boolean` に変換されたその他のデータ型 (数値型など) の値が含まれます。  
  
 `Do` ループを入れ子にするには、別のループ内にループを配置します。 また、さまざまな種類の制御構造を相互に入れ子にすることもできます。 詳細については、「[入れ子になった制御構造](../../programming-guide/language-features/control-flow/nested-control-structures.md)」を参照してください。  
  
> [!NOTE]
> `Do...Loop` 構造は、[While...End While ステートメント](while-end-while-statement.md)よりも柔軟性があります。`condition` が `True` でなくなったとき、または初めて `True` になったときに、ループを終了するかどうかを判断できるためです。 ループの開始時または終了時に `condition` をテストすることもできます。  
  
## <a name="exit-do"></a>Exit Do  
 [Exit Do](exit-statement.md) ステートメントを使用すると、別の方法で `Do…Loop` を終了させることができます。 `Exit Do` は `Loop` ステートメントの次のステートメントに制御を直ちに渡します。  
  
 `Exit Do` は、何らかの条件を評価した (`If...Then...Else` 構造など) 後によく使用されます。 誤った値や終了要求など、反復処理を続行することが不要であるか、不可能である状況が検出された場合に、ループを終了させることができます。 `Exit Do` の用途の 1 つとしては、*無限ループ*を引き起こす可能性がある条件をテストすることがあります。無限ループは、膨大な回数または無限に実行されるループです。 `Exit Do` を使用すると、ループを終了できます。  
  
 `Do…Loop` 内の任意の場所に、任意の数の `Exit Do` ステートメントを含めることができます。  
  
 入れ子になった `Do` ループ内で使用した場合、`Exit Do` は最も内側のループから次の上位レベルの入れ子に制御を渡します。  
  
## <a name="example"></a>例  
 次の例では、ループ内のステートメントは `index` 変数が 10 を超えるまで実行されます。 `Until` 句はループの最後にあります。  
  
 [!code-vb[VbVbalrStatements#131](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#131)]  
  
## <a name="example"></a>例  
 次の例では、`Until` 句ではなく `While` 句が使用されています。`condition` はループの終了時ではなく開始時にテストされます。  
  
 [!code-vb[VbVbalrStatements#132](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#132)]  
  
## <a name="example"></a>例  
 次の例では、`index` 変数が 100 を超えた場合、`condition` によってループが停止します。 ただし、ループ内の `If` ステートメントでは、インデックス変数が 10 より大きい場合、`Exit Do` ステートメントによってループが停止します。  
  
 [!code-vb[VbVbalrStatements#133](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#133)]  
  
## <a name="example"></a>例  
 次の例では、テキスト ファイル内のすべての行を読み取ります。 <xref:System.IO.File.OpenText%2A> メソッドは、ファイルを開いて、文字を読み取る <xref:System.IO.StreamReader> を返します。 `Do...Loop` 条件では、`StreamReader` の <xref:System.IO.StreamReader.Peek%2A> メソッドによって、追加の文字があるかどうかが判別されます。  
  
 [!code-vb[VbVbalrStatements#134](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#134)]  
  
## <a name="see-also"></a>関連項目

- [ループ構造](../../programming-guide/language-features/control-flow/loop-structures.md)
- [For...Next ステートメント](for-next-statement.md)
- [Boolean データ型](../data-types/boolean-data-type.md)
- [入れ子になった制御構造](../../programming-guide/language-features/control-flow/nested-control-structures.md)
- [Exit ステートメント](exit-statement.md)
- [While...End While ステートメント](while-end-while-statement.md)
