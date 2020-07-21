---
title: While...End While ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.While
- vb.While...EndWhile
helpviewer_keywords:
- While statement [Visual Basic], While...End While
- While statement [Visual Basic]
- While...End While statements [Visual Basic]
ms.assetid: b931d1ce-e8ed-44d8-a13d-92a4f5458a1e
ms.openlocfilehash: d9eb8cb95d46e860aa127954d7b44e37991d4a13
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84391587"
---
# <a name="whileend-while-statement-visual-basic"></a>While...End While ステートメント (Visual Basic)
指定された条件が `True` である限り、一連のステートメントを実行します。  
  
## <a name="syntax"></a>構文  
  
```vb  
While condition  
    [ statements ]  
    [ Continue While ]  
    [ statements ]  
    [ Exit While ]  
    [ statements ]  
End While  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`condition`|必須です。 `Boolean` 式。 `condition` が `Nothing` の場合、Visual Basic ではそれを `False` として扱います。|  
|`statements`|任意。 `While` の後の 1 つ以上のステートメント。`condition` が `True` であるたびに実行されます。|  
|`Continue While`|任意。 `While` ブロックの次の反復に制御を渡します。|  
|`Exit While`|任意。 `While` ブロックから制御を渡します。|  
|`End While`|必須です。 `While` ブロックの定義を終了します。|  
  
## <a name="remarks"></a>Remarks  
 条件が `True` のままである限り、一連のステートメントを無限に繰り返す場合は、`While...End While` 構造体を使用します。 条件をテストする場所またはテストで求める結果に関してより柔軟性を必要とする場合は、[Do...Loop ステートメント](do-loop-statement.md)を使用することをお勧めします。 設定した回数だけステートメントを繰り返す場合は、通常、[For...Next ステートメント](for-next-statement.md)の方が適しています。  
  
> [!NOTE]
> `While` キーワードは、[Do...Loop ステートメント](do-loop-statement.md)、[Skip While 句](../queries/skip-while-clause.md)、および [Take While 句](../queries/take-while-clause.md)でも使用します。  
  
 `condition` が `True` である場合、`End While` ステートメントが検出されるまで、すべての `statements` が実行されます。 その後、制御が `While` ステートメントに戻り、`condition` が再度チェックされます。 `condition` がまだ `True` である場合は、プロセスが繰り返されます。 `False` である場合は、制御が `End While` ステートメントの後のステートメントに渡されます。  
  
 `While` ステートメントでは、ループを開始する前に常に条件がチェックされます。 ループは、条件が `True` のままである間続行されます。 最初にループに入ったときに `condition` が `False` である場合は、1 回も実行されません。  
  
 通常、`condition` は 2 つの値の比較の結果になりますが、[ブール データ型](../data-types/boolean-data-type.md)の値 (`True` または `False`) に評価される任意の式を使用することもできます。 この式には、`Boolean` に変換された別のデータ型 (数値型など) の値を含めることができます。  
  
 `While` ループを入れ子にするには、別のループ内にループを配置します。 また、さまざまな種類の制御構造を相互に入れ子にすることもできます。 詳細については、「[入れ子になった制御構造](../../programming-guide/language-features/control-flow/nested-control-structures.md)」を参照してください。  
  
## <a name="exit-while"></a>Exit While  
 [Exit While](exit-statement.md) ステートメントでは、`While` ループを終了する別の方法を提供できます。 `Exit While` では `End While` ステートメントの次のステートメントに制御が直ちに渡されます。  
  
 `Exit While` は一般に、何らかの条件を評価した (`If...Then...Else` ストラクチャなどで) 後に使用します。 誤った値や終了要求など、反復処理を続行することが不要になるか、不可能になる状況を検出した場合に、ループを終了させたいことがあります。 `Exit While` は、*無限ループ*を引き起こす可能性がある条件をテストする場合に使用できます。無限ループは、膨大な回数または無限に実行する可能性があるループです。 そこで、`Exit While` を使用すると、ループから抜け出すことができます。  
  
 `While` ループ内の任意の場所に、任意の数の `Exit While` ステートメントを配置できます。  
  
 入れ子になった `While` ループ内で使用した場合、`Exit While` では最も内側のループから次の上位レベルの入れ子に制御が渡されます。  
  
 `Continue While` ステートメントでは、ループの次の反復に直ちに制御が渡されます。 詳細については、「[Continue ステートメント](continue-statement.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、ループ内のステートメントは `index` 変数が 10 を超えるまで実行されます。  
  
 [!code-vb[VbVbalrStatements#171](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class14.vb#171)]  
  
## <a name="example"></a>例  
 次の例では、`Continue While` および `Exit While` ステートメントの使用方法を示しています。  
  
 [!code-vb[VbVbalrStatements#172](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class14.vb#172)]  
  
## <a name="example"></a>例  
 次の例では、テキスト ファイル内のすべての行を読み取っています。 <xref:System.IO.File.OpenText%2A> メソッドでは、ファイルを開いて、文字を読み取る <xref:System.IO.StreamReader> が返されます。 `While` 条件では、`StreamReader` の <xref:System.IO.StreamReader.Peek%2A> メソッドによって、ファイルに追加の文字が含まれるかどうかが判断されます。  
  
 [!code-vb[VbVbalrStatements#173](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class14.vb#173)]  
  
## <a name="see-also"></a>関連項目

- [ループ構造](../../programming-guide/language-features/control-flow/loop-structures.md)
- [Do...Loop ステートメント](do-loop-statement.md)
- [For...Next ステートメント](for-next-statement.md)
- [Boolean データ型](../data-types/boolean-data-type.md)
- [入れ子になった制御構造](../../programming-guide/language-features/control-flow/nested-control-structures.md)
- [Exit ステートメント](exit-statement.md)
- [Continue ステートメント](continue-statement.md)
