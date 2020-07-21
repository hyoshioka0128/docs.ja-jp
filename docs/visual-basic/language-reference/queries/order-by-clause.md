---
title: Order By 句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryOrderBy
- vb.QueryAscending
- vb.QueryDescending
helpviewer_keywords:
- queries [Visual Basic], Order By
- Order By clause [Visual Basic]
- Order By statement [Visual Basic]
ms.assetid: fa911282-6b81-44c7-acfa-46b5bb93df75
ms.openlocfilehash: 63f454064e88bc18f252940f3abd8e59b8900e5b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359749"
---
# <a name="order-by-clause-visual-basic"></a>Order By 句 (Visual Basic)
クエリ結果の並べ替え順序を指定します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Order By orderExp1 [ Ascending | Descending ] [, orderExp2 [...] ]  
```  
  
## <a name="parts"></a>指定項目  
 `orderExp1`  
 必須です。 返される値の順序付け方法を示す、現在のクエリ結果の 1 つまたは複数のフィールド。 フィールド名は、コンマ (,) で区切る必要があります。 `Ascending` または `Descending` キーワードを使用して、昇順または降順で並べ替えて各フィールドを識別できます。 `Ascending` または `Descending` キーワードが指定されていない場合、既定の並べ替え順序は昇順です。 並べ替え順序のフィールドは、左から右に優先されます。  
  
## <a name="remarks"></a>Remarks  
 `Order By` 句を使用して、クエリの結果を並べ替えることができます。 `Order By` 句では、現在のスコープの範囲変数に基づいてのみ結果を並べ替えることができます。 たとえば、`Select` 句では、クエリ式に新しいスコープを導入し、そのスコープの新しい繰り返し変数を指定します。 クエリ内の `Select` 句の前に定義された範囲変数は、`Select` 句の後では使用できません。 そのため、`Select` 句で使用できないフィールドで結果を並べ替える場合は、`Order By` 句を `Select` 句の前に配置する必要があります。 これを行う必要がある場合の 1 つの例は、結果の一部として返されないフィールドによってクエリを並べ替える場合です。  
  
 フィールドの昇順と降順の順序は、フィールドのデータ型の <xref:System.IComparable> インターフェイスの実装によって決まります。 データ型で <xref:System.IComparable> インターフェイスを実装していない場合、並べ替え順序は無視されます。  
  
## <a name="example"></a>例  
 次のクエリ式では、`From` 句を使用して、`books` コレクションに対して `book` 範囲変数を宣言しています。 `Order By` 句によって、クエリの結果を価格の昇順で並べ替えます (既定値)。 同じ価格の書籍は、タイトルの昇順で並べ替えます。 `Select` 句によって、クエリで返される値として `Title` および `Price` プロパティを選択します。  
  
 [!code-vb[VbSimpleQuerySamples#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#24)]  
  
## <a name="example"></a>例  
 次のクエリ式では、`Order By` 句を使用して、クエリ結果を価格の降順で並べ替えています。 同じ価格の書籍は、タイトルの昇順で並べ替えます。  
  
 [!code-vb[VbSimpleQuerySamples#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#25)]  
  
## <a name="example"></a>例  
 次のクエリ式では、`Select` 句を使用して、書籍のタイトル、価格、発行日、および作者を選択しています。 次に、新しいスコープの範囲変数の `Title`、`Price`、`PublishDate`、および `Author` の各フィールドを設定します。 `Order By` 句によって、作成者名、書籍のタイトル、さらに価格で新しい範囲変数を並べ替えます。 各列を、既定の順序 (昇順) で並べ替えます。  
  
 [!code-vb[VbSimpleQuerySamples#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#26)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [Select 句](select-clause.md)
- [From 句](from-clause.md)
