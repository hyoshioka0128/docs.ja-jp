---
title: Exit ステートメント (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Exit
helpviewer_keywords:
- execution [Visual Basic], ending
- files [Visual Basic], closing
- programs [Visual Basic], quitting
- code, exiting
- Exit statement [Visual Basic]
- program termination
- execution [Visual Basic], stopping
ms.assetid: 760bfb32-5c3f-4bdb-a432-9a6001c92db7
ms.openlocfilehash: 9c25653809c51662ea5b606ab97be6a9b50d5986
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956942"
---
# <a name="exit-statement-visual-basic"></a>Exit ステートメント (Visual Basic)

プロシージャまたはブロックを終了し、プロシージャ呼び出しまたはブロック定義に続くステートメントに制御を直ちに転送します。

## <a name="syntax"></a>構文

```vb
Exit { Do | For | Function | Property | Select | Sub | Try | While }
```

## <a name="statements"></a>ステートメント

 `Exit Do`  
 が表示されている @no__t 0 ループを直ちに終了します。 実行は、`Loop` ステートメントの後のステートメントから続行されます。 `Exit Do` は、`Do` ループ内でのみ使用できます。 入れ子になった `Do` ループ内で使用される場合、@no__t は、最も内側のループを終了し、次に高い入れ子レベルに制御を移します。

 `Exit For`  
 が表示されている @no__t 0 ループを直ちに終了します。 実行は、`Next` ステートメントの後のステートメントから続行されます。 `Exit For` は、`For`... `Next` または `For Each`... @no__t のループ内でのみ使用できます。 入れ子になった `For` ループ内で使用される場合、@no__t は、最も内側のループを終了し、次に高い入れ子レベルに制御を移します。

 `Exit Function`  
 は、表示されている @no__t 0 のプロシージャを直ちに終了します。 実行は、`Function` プロシージャを呼び出したステートメントの後に続くステートメントから続行されます。 `Exit Function` は、`Function` プロシージャ内でのみ使用できます。

 戻り値を指定するには、`Exit Function` ステートメントの前にある行の関数名に値を代入します。 戻り値を割り当てて、1つのステートメントで関数を終了するには、代わりに[Return ステートメント](return-statement.md)を使用できます。

 `Exit Property`  
 は、表示されている @no__t 0 のプロシージャを直ちに終了します。 実行は、@no__t 0 プロシージャを呼び出したステートメント、つまり、プロパティの値を要求または設定するステートメントを使用して続行されます。 `Exit Property` は、プロパティの `Get` または `Set` プロシージャ内でのみ使用できます。

 @No__t-0 プロシージャで戻り値を指定するには、`Exit Property` ステートメントの前にある行の関数名に値を割り当てることができます。 戻り値を割り当てて、1つのステートメントで `Get` プロシージャを終了するには、代わりに `Return` ステートメントを使用できます。

 @No__t 0 のプロシージャでは、`Exit Property` ステートメントは `Return` ステートメントと同じです。

 `Exit Select`  
 が表示されている @no__t 0 ブロックを直ちに終了します。 実行は、`End Select` ステートメントの後のステートメントから続行されます。 `Exit Select` は、`Select Case` ステートメント内でのみ使用できます。

 `Exit Sub`  
 は、表示されている @no__t 0 のプロシージャを直ちに終了します。 実行は、`Sub` プロシージャを呼び出したステートメントの後に続くステートメントから続行されます。 `Exit Sub` は、`Sub` プロシージャ内でのみ使用できます。

 @No__t 0 のプロシージャでは、`Exit Sub` ステートメントは `Return` ステートメントと同じです。

 `Exit Try`  
 が表示されている @no__t 0 または `Catch` ブロックを直ちに終了します。 実行は、`Finally` ブロックがある場合は、それ以外の場合は `End Try` ステートメントの後に続くステートメントで続行されます。 `Exit Try` は、`Finally` ブロック内ではなく、`Try` または `Catch` ブロック内でのみ使用できます。

 `Exit While`  
 が表示されている @no__t 0 ループを直ちに終了します。 実行は、`End While` ステートメントの後のステートメントから続行されます。 `Exit While` は、`While` ループ内でのみ使用できます。 入れ子になった `While` ループ内で使用される場合、`Exit While` は、`Exit While` が発生するループの上に入れ子になった1つのレベルを持つループに制御を転送します。

## <a name="remarks"></a>コメント

@No__t-0 ステートメントと `End` ステートメントを混同しないようにしてください。 `Exit` はステートメントの末尾を定義しません。

## <a name="example"></a>例

次の例では、@no__t 0 の変数が100より大きい場合、ループ条件によってループが停止します。 ただし、ループ内の `If` ステートメントを指定すると、インデックス変数が10より大きい場合に、`Exit Do` ステートメントによってループが停止します。

[!code-vb[VbVbalrStatements#133](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#133)]

## <a name="example"></a>例

次の例では、関数名 `myFunction` に戻り値を代入した後、`Exit Function` を使用して関数から戻ります。

[!code-vb[VbVbalrStatements#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#23)]

## <a name="example"></a>例

次の例では、 [Return ステートメント](return-statement.md)を使用して戻り値を割り当て、関数を終了します。

[!code-vb[VbVbalrStatements#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#24)]

## <a name="see-also"></a>関連項目

- [Continue ステートメント](continue-statement.md)
- [Do...Loop ステートメント](do-loop-statement.md)
- [End ステートメント](end-statement.md)
- [For Each...Next ステートメント](for-each-next-statement.md)
- [For...Next ステートメント](for-next-statement.md)
- [Function ステートメント](function-statement.md)
- [Return ステートメント](return-statement.md)
- [Stop ステートメント](stop-statement.md)
- [Sub ステートメント](sub-statement.md)
- [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)
