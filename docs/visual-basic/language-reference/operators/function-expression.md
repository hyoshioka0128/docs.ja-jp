---
title: Function 式
ms.date: 07/20/2015
helpviewer_keywords:
- Function expression [Visual Basic]
- functions [Visual Basic], function expressions
- lambda expressions [Visual Basic], function expression
ms.assetid: e8a47a45-4b8a-4f45-a623-7653625dffbc
ms.openlocfilehash: a9b621ff03f833fcf0f07f876fd864ee963bef75
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371182"
---
# <a name="function-expression-visual-basic"></a>Function 式 (Visual Basic)
関数ラムダ式を定義するパラメーターとコードを宣言します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Function ( [ parameterlist ] ) expression  
- or -  
Function ( [ parameterlist ] )  
  [ statements ]  
End Function  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`parameterlist`|任意。 このプロシージャのパラメーターを表すローカル変数名のリスト。 リストが空の場合でも、かっこが存在する必要があります。 「[パラメーター リスト](../statements/parameter-list.md)」を参照してください。|  
|`expression`|必須です。 単一の式。 式の型は、関数の戻り値の型です。|  
|`statements`|必須です。 `Return` ステートメントを使用して値を返すステートメントのリスト。 (「[Return ステートメント](../statements/return-statement.md)」を参照してください。)戻される値の型は、関数の戻り値の型です。|  
  
## <a name="remarks"></a>Remarks  
 *ラムダ式*は、値を計算して返す、名前を持たない関数です。 ラムダ式は、デリゲート型を使用できる場所であればどこでも使用できます。ただし、`RemoveHandler` の引数として使用することはできません。 デリゲートの詳細と、デリゲートでのラムダ式の使用の詳細については、「[Delegate ステートメント](../statements/delegate-statement.md)」と「[厳密でないデリゲート変換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)」をご覧ください。  
  
## <a name="lambda-expression-syntax"></a>ラムダ式の構文  
 ラムダ式の構文は、標準の関数の構文に似ています。 相違点は、次のとおりです。  
  
- ラムダ式には名前はありません。  
  
- ラムダ式には、`Overloads` や `Overrides` などの修飾子を含めることはできません。  
  
- ラムダ式では、関数の戻り値の型を指定するために `As` 句は使用されません。 代わりに、単一行のラムダ式の本体が評価された結果の値、または複数行のラムダ式の戻り値から型が推論されます。 たとえば、単一行のラムダ式の本体が `Where cust.City = "London"` の場合、戻り値の型は `Boolean` になります。  
  
- 単一行のラムダ式の本体は、ステートメントではなく、式でなければなりません。 本体は、関数プロシージャの呼び出しで構成できますが、サブ プロシージャの呼び出しでは構成できません。  
  
- すべてのパラメーターにデータ型が指定されているか、すべてが推論される必要があります。  
  
- 省略可能なパラメーターと Paramarray パラメーターは使用できません。  
  
- ジェネリック パラメーターは使用できません。  
  
## <a name="example"></a>例  
 次の例は、単純なラムダ式を作成する 2 つの方法を示しています。 最初の方法では、`Dim` を使用して関数の名前を指定しています。 関数を呼び出すには、パラメーターの値を送信します。  
  
 [!code-vb[VbVbalrLambdas#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#1)]  
  
 [!code-vb[VbVbalrLambdas#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#2)]  
  
## <a name="example"></a>例  
 別の方法として、関数の宣言と実行を同時に行うこともできます。  
  
 [!code-vb[VbVbalrLambdas#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#3)]  
  
## <a name="example"></a>例  
 次の例は、引数をインクリメントして値を返すラムダ式です。 この例は、関数の単一行および複数行のラムダ式の構文を示しています。 その他の例については、「[ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)」を参照してください。  
  
 [!code-vb[VbVbalrLambdas#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#14)]  
  
## <a name="example"></a>例  
 ラムダ式は、統合言語クエリ (LINQ) のクエリ演算子の多くを基にしており、メソッド ベースのクエリで明示的に使用できます。 次の例は、一般的な LINQ クエリを示し、続いてそのクエリをメソッド形式のクエリに変換する方法を示しています。  
  
```vb  
Dim londonCusts = From cust In db.Customers  
                       Where cust.City = "London"  
                       Select cust  
  
' This query is compiled to the following code:  
Dim londonCusts = db.Customers.  
                  Where(Function(cust) cust.City = "London").  
                  Select(Function(cust) cust)  
```  
  
 クエリ メソッドの詳細については、「[クエリ](../queries/index.md)」を参照してください。 標準クエリ演算子の詳細については、「[標準クエリ演算子の概要](../../programming-guide/concepts/linq/standard-query-operators-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Function ステートメント](../statements/function-statement.md)
- [ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)
- [演算子および式](../../programming-guide/language-features/operators-and-expressions/index.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
- [値の比較](../../programming-guide/language-features/operators-and-expressions/value-comparisons.md)
- [ブール式](../../programming-guide/language-features/operators-and-expressions/boolean-expressions.md)
- [If 演算子](if-operator.md)
- [厳密でないデリゲート変換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
