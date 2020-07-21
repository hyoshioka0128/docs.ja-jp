---
title: Where 句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryWhere
helpviewer_keywords:
- Where statement [Visual Basic]
- queries [Visual Basic], Where
- Where clause [Visual Basic]
ms.assetid: 48b5c2c5-3181-429c-8545-894296798c89
ms.openlocfilehash: b80bb047551dee8ab23cfac06b961996992d69b5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359542"
---
# <a name="where-clause-visual-basic"></a>Where 句 (Visual Basic)
クエリのフィルター処理条件を示します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Where condition  
```  
  
## <a name="parts"></a>指定項目  
 `condition`  
 必須です。 コレクション内の現在の項目の値が出力コレクションに含まれるかどうかを決定する式。 式は、`Boolean` 値または `Boolean` 値と等価の値に評価される必要があります。 条件が `True` に評価される場合、要素はクエリ結果に含まれます。それ以外の場合、要素はクエリ結果から除外されます。  
  
## <a name="remarks"></a>Remarks  
 `Where` 句を使用すると、特定の条件を満たす要素のみを選択することで、クエリ データをフィルター処理できます。 値が `Where` 句を `True` に評価させる要素は、クエリ結果に含まれます。その他の要素は除外されます。 `Where` 句で使用される式は、`Boolean` または `Boolean` と等価 (値が 0 の場合に `False` に評価される整数など) に評価される必要があります。 `Where` 句では、`And`、`Or`、`AndAlso`、`OrElse`、`Is`、`IsNot` などの論理演算子を使用して、複数の式を組み合わせることができます。  
  
 既定では、クエリ式は、アクセスされるまで評価されません。たとえば、データ バインドされたり、`For` ループ内で反復処理されたりするときです。 その結果、`Where` 句は、クエリがアクセスされるまで評価されません。 `Where` 句で使用されているクエリの外部の値がある場合は、クエリの実行時に `Where` 句で適切な値が使用されていることを確認してください。 クエリの実行の詳細については、「[初めての LINQ クエリの作成](../../programming-guide/concepts/linq/writing-your-first-linq-query.md)」を参照してください。  
  
 `Where` 句内で関数を呼び出して、コレクション内の現在の要素の値に対して計算または操作を実行することができます。 `Where` 句で関数を呼び出すと、クエリを、アクセス時ではなく定義された直後に実行することができます。 クエリの実行の詳細については、「[初めての LINQ クエリの作成](../../programming-guide/concepts/linq/writing-your-first-linq-query.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のクエリ式では、`From` 句を使用して、`customers` コレクション内の各 `Customer` オブジェクトに対して `cust` 範囲変数を宣言しています。 `Where` 句では、範囲変数を使用して、指定した地域の顧客に出力を制限します。 `For Each` ループによって、クエリ結果に各顧客の会社名を表示します。  
  
 [!code-vb[VbSimpleQuerySamples#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#23)]  
  
## <a name="example"></a>例  
 次の例では、`Where` 句で `And` および `Or` 論理演算子を使用しています。  
  
 [!code-vb[VbSimpleQuerySamples#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#31)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [From 句](from-clause.md)
- [Select 句](select-clause.md)
- [For Each...Next ステートメント](../statements/for-each-next-statement.md)
