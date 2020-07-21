---
title: Aggregate Clause
ms.date: 08/28/2018
f1_keywords:
- vb.QueryAggregateIn
- vb.QueryAggregate
- vb.QueryAggregateInto
helpviewer_keywords:
- Aggregate clause [Visual Basic]
- Aggregate statement [Visual Basic]
- queries [Visual Basic], Aggregate
ms.assetid: 1315a814-5db6-4077-b34b-b141e11cc0eb
ms.openlocfilehash: 326c3306368ceca2122e912556efd84e4bfef1f1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413002"
---
# <a name="aggregate-clause-visual-basic"></a>Aggregate 句 (Visual Basic)
1 つ以上の集計関数をコレクションに適用します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Aggregate element [As type] In collection _  
  [, element2 [As type2] In collection2, [...]]  
  [ clause ]  
  Into expressionList  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`element`|必須です。 コレクションの要素の反復処理に使用される変数。|  
|`type`|任意。 `element` の型。 型が指定されていない場合、`element` の型は `collection` から推論されます。|  
|`collection`|必須です。 操作対象のコレクションを参照します。|  
|`clause`|任意。 Aggregate 句を適用するクエリ結果を絞り込むための `Where` 句などの 1 つ以上のクエリ句。|  
|`expressionList`|必須です。 コレクションに適用する集計関数を識別する 1 つ以上のコンマ区切り式。 集計関数に別名を適用して、クエリ結果のメンバー名を指定できます。 別名が指定されていない場合、集計関数の名前が使用されます。 例については、このトピックで後述する集計関数に関するセクションを参照してください。|  
  
## <a name="remarks"></a>Remarks  
 `Aggregate` 句を使用して、クエリに集計関数を含めることができます。 集計関数は、値の集まりに対して、チェックと計算を実行し、1 つの値を返します。 クエリ結果の型のメンバーを使用して、計算された値にアクセスできます。 使用できる標準の集計関数は、`All`、`Any`、`Average`、`Count`、`LongCount`、`Max`、`Min`、`Sum` 関数です。 これらの関数は、SQL での集計に精通している開発者になじみがあります。 このトピックの以降のセクションで、それらについて説明します。  
  
 集計関数の結果は、クエリ結果の型のフィールドとしてクエリ結果に含まれます。 集計関数の結果に別名を指定して、集計値を保持するクエリ結果の型のメンバーの名前を指定できます。 別名が指定されていない場合、集計関数の名前が使用されます。  
  
 `Aggregate` 句は、クエリを開始したり、クエリの追加の句として含めたりすることができます。 `Aggregate` 句によってクエリが開始された場合、結果は、`Into` 句に指定された集計関数の結果である単一の値になります。 `Into` 句に複数の集計関数が指定されている場合、クエリでは、`Into` 句で各集計関数の結果を参照するための個別のプロパティを持つ単一の型が返されます。 `Aggregate` 句がクエリに追加の句として含まれている場合、クエリ コレクションで返される型には、`Into` 句で各集計関数の結果を参照する個別のプロパティがあります。  
  
## <a name="aggregate-functions"></a>集計関数

次に、`Aggregate` 句で使用できる標準の集計関数を示します。  
  
### <a name="all"></a>すべて

コレクション内のすべての要素が指定された条件を満たす場合に `true` を返します。それ以外の場合は `false` を返します。 次に例を示します。

 [!code-vb[VbSimpleQuerySamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#5)]

### <a name="any"></a>どれでも可

コレクション内のいずれかの要素が指定された条件を満たす場合に `true` を返します。それ以外の場合は `false` を返します。 次に例を示します。

 [!code-vb[VbSimpleQuerySamples#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#6)]

### <a name="average"></a>平均

コレクション内のすべての要素の平均値を計算するか、コレクション内のすべての要素に対して指定された式を計算します。 次に例を示します。

 [!code-vb[VbSimpleQuerySamples#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#7)]

### <a name="count"></a>カウント

コレクション内の要素の数をカウントします。 条件を満たすコレクション内の要素の数のみをカウントする省略可能な `Boolean` 式を指定できます。 次に例を示します。

 [!code-vb[VbSimpleQuerySamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#8)]

### <a name="group"></a>グループ化

`Group By` または `Group Join` 句の結果として、グループ化されたクエリ結果を参照します。 `Group` 関数は、`Group By` または `Group Join` 句の `Into` 句でのみ有効です。 詳細と例については、「[Group By 句](group-by-clause.md)」と「[Group Join 句](group-join-clause.md)」を参照してください。

### <a name="longcount"></a>LongCount

コレクション内の要素の数をカウントします。 条件を満たすコレクション内の要素の数のみをカウントする省略可能な `Boolean` 式を指定できます。 結果を `Long` として返します。 例については、「`Count` 集計関数」を参照してください。

### <a name="max"></a>最大

コレクションから最大値を計算するか、コレクション内のすべての要素に対して指定された式を計算します。 次に例を示します。

 [!code-vb[VbSimpleQuerySamples#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#9)]

### <a name="min"></a>最小

コレクションから最小値を計算するか、コレクション内のすべての要素に対して指定された式を計算します。 次に例を示します。

 [!code-vb[VbSimpleQuerySamples#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#10)]

### <a name="sum"></a>Sum

コレクション内のすべての要素の合計を計算するか、コレクション内のすべての要素に対して指定された式を計算します。 次に例を示します。

 [!code-vb[VbSimpleQuerySamples#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#15)]

## <a name="example"></a>例  

次の例では、`Aggregate` 句を使用して、クエリ結果に集計関数を適用する方法を示します。  
  
 [!code-vb[VbSimpleQuerySamples#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#4)]  
  
## <a name="creating-user-defined-aggregate-functions"></a>ユーザー定義集計関数の作成

 <xref:System.Collections.Generic.IEnumerable%601> 型に拡張メソッドを追加することで、独自のカスタム集計関数をクエリ式に含めることができます。 カスタム メソッドが、集計関数を参照した列挙可能なコレクションに対して計算や操作を実行できるようになります。 拡張メソッドについて詳しくは、「[拡張メソッド](../../programming-guide/language-features/procedures/extension-methods.md)」をご覧ください。  
  
 たとえば、次の例では、数値のコレクションの中央値を計算するカスタム集計関数を示しています。 `Median` 拡張メソッドには、2 つのオーバーロードがあります。 最初のオーバーロードでは、入力として `IEnumerable(Of Double)` 型のコレクションを受け入れます。 `Double` 型のクエリ フィールドに対して `Median` 集計関数が呼び出されると、このメソッドが呼び出されます。 `Median` メソッドの 2 つ目のオーバーロードには、任意のジェネリック型を渡すことができます。 `Median` メソッドのジェネリック オーバーロードは、`Func(Of T, Double)` ラムダ式を参照する 2 つ目のパラメーターを受け取ります。このパラメーターは、ある型 (コレクションからの) の値を `Double` 型の対応する値としてプロジェクションします。 次に、中央値の計算を `Median` メソッドの他のオーバーロードにデリゲートします。 ラムダ式について詳しくは、「[ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)」をご覧ください。  
  
 [!code-vb[VbSimpleQuerySamples#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/UserDefinedAggregates.vb#18)]  
  
 次の例は、`Integer` 型のコレクションと `Double` 型のコレクションに対して `Median` 集計関数を呼び出すサンプル クエリを示しています。 `Double` 型のコレクションに対して `Median` 集計関数を呼び出すクエリは、`Double` 型のコレクションを入力として受け入れる `Median` メソッドのオーバーロードを呼び出します。 `Integer` 型のコレクションに対して `Median` 集計関数を呼び出すクエリは、`Median` メソッドのジェネリック オーバーロードを呼び出します。  
  
 [!code-vb[VbSimpleQuerySamples#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/UserDefinedAggregates.vb#19)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [Select 句](select-clause.md)
- [From 句](from-clause.md)
- [WHERE 句](where-clause.md)
- [Group By 句](group-by-clause.md)
