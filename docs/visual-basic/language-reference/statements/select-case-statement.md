---
title: Select...Case ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.Select
- vb.Case
helpviewer_keywords:
- Select statement [Visual Basic]
- Case statement [Visual Basic]
- Select...Case statements
- conditional statements [Visual Basic], Select Case
- control flow [Visual Basic], branching
- Else keyword [Visual Basic], in Select...Case statements
- execution [Visual Basic], conditional
- To keyword [Visual Basic], in Select...Case statements
- Select Case statement [Visual Basic], Select...Case
- Select statement [Visual Basic], Select...Case
- Is operator [Visual Basic], in Select...Case statements
- branching [Visual Basic], conditional
- Case Else statement [Visual Basic], Select...Case
- End keyword [Visual Basic], Select Case statements
- Case statement [Visual Basic], Select...Case
ms.assetid: 68877b65-5419-4bf0-a465-20cd0e4c7d44
ms.openlocfilehash: 3dedd43f920b493a0aca9ce48460b00815e1af5c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404240"
---
# <a name="selectcase-statement-visual-basic"></a>Select...Case ステートメント (Visual Basic)
式の値に応じて、いくつかのステートメント グループのいずれかを実行します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Select [ Case ] testexpression  
    [ Case expressionlist  
        [ statements ] ]  
    [ Case Else  
        [ elsestatements ] ]  
End Select  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`testexpression`|必須です。 式。 基本データ型 (`Boolean`、`Byte`、`Char`、`Date`、`Double`、`Decimal`、`Integer`、`Long`、`Object`、`SByte`、`Short`、`Single`、`String`、`UInteger`、`ULong`、および `UShort`) のいずれかとして評価される必要があります。|  
|`expressionlist`|`Case` ステートメントには必ず指定します。 `testexpression` の一致する値を表す式の句の一覧。 複数の式の句を指定するときは、コンマで区切ります。 各句には、次のいずれかの形式を使用できます。<br /><br /> -   *expression1* `To` *expression2*<br />-   [ `Is` ] *comparisonoperator* *expression*<br />-   *式*<br /><br /> `To` キーワードを使用して、`testexpression` の一致する値の範囲の境界を指定します。 `expression1` の値は `expression2` の値以下である必要があります。<br /><br /> 比較演算子 (`=`、`<>`、`<`、`<=`、`>`、または `>=`) と共に `Is` キーワードを使用して、`testexpression` の一致する値に対する制限を指定します。 `Is` キーワードが指定されていない場合は、自動的に *comparisonoperator* の前に挿入されます。<br /><br /> `expression` のみを指定する形式は、`Is` 形式の特殊なケースとして扱われます。ここで、*comparisonoperator* は等号 (`=`) です。 この形式は `testexpression` = `expression` として評価されます。<br /><br /> `expressionlist` の式は、`testexpression` の型に暗黙的に変換可能であり、一緒に使用される 2 つの型に対して適切な `comparisonoperator` が有効であれば、任意のデータ型にすることができます。|  
|`statements`|任意。 `testexpression` が `expressionlist` 内のいずれかの句と一致する場合に実行される、`Case` の後の 1 つ以上のステートメント。|  
|`elsestatements`|任意。 `testexpression` が どの `Case` ステートメントの `expressionlist` 内のどの句とも一致しない場合に実行される、`Case Else` の後の 1 つ以上のステートメント。|  
|`End Select`|`Select`...`Case` コンストラクションの定義を終了します。|  
  
## <a name="remarks"></a>Remarks  
 `testexpression` が `Case` `expressionlist` 句と一致する場合、その `Case` ステートメントの後のステートメントは、次の `Case`、`Case Else`、または `End Select` ステートメントまで実行されます。 その後、制御は `End Select` の後のステートメントに渡されます。 `testexpression` が複数の `Case` 句の `expressionlist` 句と一致する場合は、最初の一致の後のステートメントのみが実行されます。  
  
 `Case Else` ステートメントを使用して、他のいずれかの `Case` ステートメントで `testexpression` 句と `expressionlist` 句の間に一致が検出されなかった場合に実行する `elsestatements` を導入します。 必須ではありませんが、予期しない `testexpression` 値を処理するために、`Select Case` コンストラクションに `Case Else` ステートメントを指定することをお勧めします。 `Case` `expressionlist` 句が `testexpression` に一致せず、`Case Else` ステートメントが存在しない場合、制御は `End Select` の後のステートメントに渡されます。  
  
 各 `Case` 句では、複数の式または範囲を使用できます。 たとえば、次の行は有効です。  
  
 `Case 1 To 4, 7 To 9, 11, 13, Is > maxNumber`  
  
> [!NOTE]
> `Case` および `Case Else` ステートメントで使用される `Is` キーワードは、オブジェクト参照の比較に使用される [Is Operator](../operators/is-operator.md) と同じではありません。  
  
 文字列の範囲と複数の式を指定できます。 次の例では、`Case` は、"apples" と完全に等しいか、アルファベット順の "nuts" と "soup" の間の値を持つか、`testItem` の現在の値とまったく同じ値が含まれている任意の文字列に一致します。  
  
 `Case "apples", "nuts" To "soup", testItem`  
  
 `Option Compare` の設定は、文字列比較に影響を与える可能性があります。 `Option Compare Text` では、文字列 "Apples" と "apples" は等しいものとして比較されますが、`Option Compare Binary` ではこれらは等しくありません。  
  
> [!NOTE]
> 複数の句を持つ `Case` ステートメントでは、*ショートサーキット*と呼ばれる動作が発生する可能性があります。 Visual Basic では句が左から右に評価され、いずれかが `testexpression` と一致する場合、残りの句は評価されません。 ショートサーキットはパフォーマンスを向上させることができますが、`expressionlist` 内のすべての式を評価する必要がある場合は、予期しない結果が生じる可能性があります。 ショートサーキットの詳細については、[ブール式](../../programming-guide/language-features/operators-and-expressions/boolean-expressions.md)に関するページを参照してください。  
  
 `Case` または `Case Else` ステートメント ブロック内のコードがブロック内のステートメントをこれ以上実行する必要がない場合は、`Exit Select` ステートメントを使用してブロックを終了できます。 これは `End Select` の次のステートメントに制御を直ちに渡します。  
  
 `Select Case` コンストラクションは入れ子にできます。 入れ子になった `Select Case` コンストラクションのそれぞれには、一致する `End Select` ステートメントが必要です。また、入れ子になっている外側の `Select Case` コンストラクションの 1 つの `Case` または `Case Else` ステートメント ブロック内に完全に含まれている必要があります。  
  
## <a name="example"></a>例  
 次の例では、`Select Case` コンストラクションを使用して、変数 `number` の値に対応する行を記述します。 2 番目の `Case` ステートメントには、`number` の現在の値と一致する値が含まれています。そのため、"Between 6 and 8, inclusive" を記述するステートメントが実行されます。  
  
 [!code-vb[VbVbalrStatements#54](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#54)]  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Interaction.Choose%2A>
- [End ステートメント](end-statement.md)
- [If...Then...Else ステートメント](if-then-else-statement.md)
- [Option Compare ステートメント](option-compare-statement.md)
- [Exit ステートメント](exit-statement.md)
