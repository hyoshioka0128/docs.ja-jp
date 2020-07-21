---
title: Join 句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryJoinIn
- vb.QueryJoin
- vb.QueryJoinOn
helpviewer_keywords:
- queries [Visual Basic], Join
- Join statement [Visual Basic]
- Join clause [Visual Basic]
ms.assetid: 6dd37936-b27c-4e00-98ad-154b23f4de64
ms.openlocfilehash: f73dc31bbbb9014a8a1a315de406c53fa58d1c65
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359775"
---
# <a name="join-clause-visual-basic"></a>Join 句 (Visual Basic)

2 つのコレクションを単一のコレクションに結合します。 結合操作は、一致するキーに基づき、`Equals` 演算子を使用します。

## <a name="syntax"></a>構文

```vb
Join element In collection _
  [ joinClause _ ]
  [ groupJoinClause ... _ ]
On key1 Equals key2 [ And key3 Equals key4 [... ]
```

## <a name="parts"></a>指定項目

`element` 必須。 結合されるコレクションの制御変数。

`collection`  
必須です。 `Join` 演算子の左側に指定されているコレクションと結合するコレクション。 `Join` 句は、別の `Join` 句、または `Group Join` 句で入れ子にすることができます。

`joinClause`  
任意。 クエリをさらに絞り込むための 1 つ以上の追加の `Join` 句。

`groupJoinClause`  
任意。 クエリをさらに絞り込むための 1 つ以上の追加の `Group Join` 句。

`key1` `Equals` `key2`  
必須です。 結合されるコレクションのキーを識別します。 `Equals` 演算子を使用して、結合されるコレクションのキーを比較する必要があります。 結合条件を組み合わせるには、複数のキーを識別するために、`And` 演算子を使用します。 `key1` は、`Join` 演算子の左側にあるコレクションのものである必要があります。 `key2` は、`Join` 演算子の右側にあるコレクションのものである必要があります。

結合条件で使用されるキーは、コレクションからの複数の項目を含む式にすることができます。 ただし、各キー式には、それぞれのコレクションの項目のみを含めることができます。

## <a name="remarks"></a>Remarks

`Join` 句は、結合されるコレクションからの一致するキー値に基づいて、2 つのコレクションを組み合わせます。 結果のコレクションには、`Join` 演算子の左側に指定されたコレクションと、`Join` 句で指定されたコレクションからの値の任意の組み合わせが含まれる可能性があります。 クエリから返されるのは、`Equals` 演算子によって指定された条件を満たした結果だけです。 これは、SQL の `INNER JOIN` と同じです。

クエリで複数の `Join` 句を使用して、複数のコレクションを 1 つのコレクションに結合できます。

暗黙的結合を実行して、`Join` 句を使用せずにコレクションを結合することができます。 これを行うには、`From` 句に複数の `In` 句を含め、結合に使用するキーを識別する `Where` 句を指定します。

`Group Join` 句を使用して、コレクションを、単一の階層コレクションに結合することができます。 これは、SQL の `LEFT OUTER JOIN` に似ています。

## <a name="example"></a>例

次のコード例では、暗黙的結合を実行して、顧客のリストと注文を結合しています。

[!code-vb[VbSimpleQuerySamples#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#13)]

## <a name="example"></a>例

次のコード例では、`Join` 句を使用して 2 つのコレクションを結合しています。

[!code-vb[VbSimpleQuerySamples#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples2.vb#12)]

この例では、次のような出力が生成されます。

`winlogon (968), Windows Logon`

`explorer (2424), File Explorer`

`cmd (5136), Command Window`

## <a name="example"></a>例

次のコード例では、2 つのキー列で `Join` 句を使用して、2 つのコレクションを結合しています。

[!code-vb[VbSimpleQuerySamples#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples3.vb#17)]

この例では、次のような出力が生成されます。

`winlogon (968), Windows Logon, Priority = 13`

`cmd (700), Command Window, Priority = 8`

`explorer (2424), File Explorer, Priority = 8`

## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [Select 句](select-clause.md)
- [From 句](from-clause.md)
- [Group Join 句](group-join-clause.md)
- [WHERE 句](where-clause.md)
