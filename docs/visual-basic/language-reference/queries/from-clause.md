---
title: From 句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryFrom
- vb.QueryFromIn
- vb.QueryFromLet
helpviewer_keywords:
- queries [Visual Basic], From
- From clause [Visual Basic]
- From statement [Visual Basic]
ms.assetid: 83e3665e-68a0-4540-a3a3-3d777a0f95d5
ms.openlocfilehash: 33680f49247b3b2a6082b3a6b27ca64f8401e42d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396182"
---
# <a name="from-clause-visual-basic"></a>From 句 (Visual Basic)
クエリを実行する 1 つ以上の範囲変数とコレクションを指定します。  
  
## <a name="syntax"></a>構文  
  
```vb  
From element [ As type ] In collection [ _ ]  
  [, element2 [ As type2 ] In collection2 [, ... ] ]  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`element`|必須です。 コレクションの要素の反復処理に使用される*範囲変数*。 範囲変数は、クエリによって `collection` を反復処理するときに、`collection` の各メンバーを参照するために使用されます。 列挙可能な型である必要があります。|  
|`type`|任意。 `element` の型。 `type` が指定されていない場合、`element` の型は `collection` から推論されます。|  
|`collection`|必須です。 クエリ対象のコレクションを参照します。 列挙可能な型である必要があります。|  
  
## <a name="remarks"></a>Remarks  
 `From` 句は、クエリのソース データと、ソース コレクションの要素を参照するために使用される変数を識別するために使用します。 このような変数は*範囲変数*と呼ばれます。 `Aggregate` 句を使用して、集計結果のみを返すクエリを識別する場合を除き、クエリには `From` 句が必要です。 詳細については、「[Aggregate 句](aggregate-clause.md)」を参照してください。  
  
 クエリで複数の `From` 句を指定して、結合する複数のコレクションを識別できます。 複数のコレクションを指定している場合、それらは個別に反復処理するか、またはそれらが関連付けられている場合は結合できます。 コレクションは、`Select` 句を使用して暗黙的に結合することも、`Join` または `Group Join` 句を使用して明示的に結合することもできます。 または、1 つの `From` 句で、関連する各範囲変数とコレクションをそれぞれコンマで区切って、複数の範囲変数とコレクションを指定することもできます。 次のコード例に、`From` 句の両方の構文オプションを示しています。  
  
 [!code-vb[VbSimpleQuerySamples#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#21)]  
  
 `From` 句は、クエリのスコープを定義します。これは、`For` ループのスコープに似ています。 そのため、クエリのスコープ内の各 `element` 範囲変数には、一意の名前を付ける必要があります。 クエリに対して複数の `From` 句を指定できるので、後続の `From` 句で `From` 句内の範囲変数を参照できます。または、前の `From` 句内の範囲変数を参照することもできます。 たとえば、次の例は、入れ子になった `From` 句を示しています。2 つ目の句のコレクションは、最初の句の範囲変数のプロパティに基づいています。  
  
 [!code-vb[VbSimpleQuerySamples#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#22)]  
  
 各 `From` 句の後に、追加のクエリ句の任意の組み合わせを指定して、クエリを絞り込むことができます。 クエリは、次の方法で絞り込むことができます。  
  
- `From` 句と `Select` 句を使用して暗黙的に、または `Join` 句または `Group Join` 句を使用して明示的に、複数のコレクションを結合します。  
  
- `Where` 句を使用して、クエリ結果をフィルター処理します。  
  
- `Order By` 句を使用して、結果を並べ替えます。  
  
- `Group By` 句を使用して、類似した結果をグループ化します。  
  
- `Aggregate` 句を使用して、クエリ結果全体を評価する集計関数を特定します。  
  
- `Let` 句を使用して、コレクションではなく式によって値が決定される反復変数を導入します。  
  
- `Distinct` 句を使用して、重複するクエリ結果を無視します。  
  
- `Skip`、`Take`、`Skip While`、および `Take While` 句を使用して、返される結果の部分を特定します。  
  
## <a name="example"></a>例  
 次のクエリ式では、`From` 句を使用して、`customers` コレクション内の各 `Customer` オブジェクトに対して `cust` 範囲変数を宣言しています。 `Where` 句では、範囲変数を使用して、指定した地域の顧客に出力を制限します。 `For Each` ループによって、クエリ結果に各顧客の会社名を表示します。  
  
 [!code-vb[VbSimpleQuerySamples#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#23)]  
  
## <a name="see-also"></a>関連項目

- [クエリ](index.md)
- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [For Each...Next ステートメント](../statements/for-each-next-statement.md)
- [For...Next ステートメント](../statements/for-next-statement.md)
- [Select 句](select-clause.md)
- [WHERE 句](where-clause.md)
- [Aggregate 句](aggregate-clause.md)
- [Distinct 句](distinct-clause.md)
- [Join 句](join-clause.md)
- [Group Join 句](group-join-clause.md)
- [Order By 句](order-by-clause.md)
- [Let 句](let-clause.md)
- [Skip 句](skip-clause.md)
- [Take 句](take-clause.md)
- [Skip While 句](skip-while-clause.md)
- [Take While 句](take-while-clause.md)
