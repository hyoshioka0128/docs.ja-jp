---
title: Group Join 句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryGroupJoinIn
- vb.QueryGroupJoinOn
- vb.QueryGroupJoin
- vb.QueryGroupJoinInto
helpviewer_keywords:
- Group Join clause [Visual Basic]
- Group Join statement [Visual Basic]
- queries [Visual Basic], Group Join
ms.assetid: 37dbf79c-7b5c-421b-bbb7-dadfd2b92a1c
ms.openlocfilehash: 7916e51293c06016b2581b7109df3f0a599404ca
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359835"
---
# <a name="group-join-clause-visual-basic"></a>Group Join 句 (Visual Basic)
2 つのコレクションを、単一の階層コレクションに結合します。 結合操作は、一致するキーに基づきます。  
  
## <a name="syntax"></a>構文  
  
```vb  
Group Join element [As type] In collection _  
  On key1 Equals key2 [ And key3 Equals key4 [... ] ] _  
  Into expressionList  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`element`|必須です。 結合されるコレクションの制御変数。|  
|`type`|任意。 `element` の型。 `type` が指定されていない場合、`element` の型は `collection` から推論されます。|  
|`collection`|必須です。 `Group Join` 演算子の左側にあるコレクションと結合するコレクション。 `Group Join` 句は、`Join` 句、または別の `Group Join` 句で入れ子にすることができます。|  
|`key1` `Equals` `key2`|必須です。 結合されるコレクションのキーを識別します。 `Equals` 演算子を使用して、結合されるコレクションのキーを比較する必要があります。 結合条件を組み合わせるには、複数のキーを識別するために、`And` 演算子を使用します。 `key1` パラメーターは、`Join` 演算子の左側にあるコレクションからのものである必要があります。 `key2` パラメーターは、`Join` 演算子の右側にあるコレクションからのものである必要があります。<br /><br /> 結合条件で使用されるキーは、コレクションからの複数の項目を含む式にすることができます。 ただし、各キー式には、それぞれのコレクションからの項目のみを含めることができます。|  
|`expressionList`|必須です。 コレクションの要素のグループを集計する方法を示す 1 つ以上の式です。 グループ化された結果のメンバー名を特定するには、`Group` キーワード (`<alias> = Group`) を使用します。 グループに適用する集計関数を含めることもできます。|  
  
## <a name="remarks"></a>Remarks  
 `Group Join` 句は、結合されるコレクションからの一致するキー値に基づいて、2 つのコレクションを組み合わせます。 結果のコレクションには、最初のコレクションのキー値に一致する 2 つ目のコレクションの要素のコレクションを参照するメンバーを含めることができます。 さらに、2 つ目のコレクションのグループ化された要素に適用する集計関数を指定することもできます。 集計関数の詳細については、「[Aggregate 句 ](aggregate-clause.md)」を参照してください。  
  
 たとえば、マネージャーのコレクションと従業員のコレクションを考えてみましょう。 両方のコレクションの要素には、特定のマネージャーに報告する従業員を識別する ManagerID プロパティがあります。 結合操作の結果には、一致する ManagerID 値を持つ各マネージャーと従業員の結果が含まれます。 `Group Join` 操作の結果には、マネージャーの完全な一覧が含まれます。 各マネージャーの結果には、特定のマネージャーに一致した従業員の一覧を参照したメンバーが含まれます。  
  
 `Group Join` 操作の結果のコレクションには、`From` 句に指定されたコレクションと `Group Join` 句の `Into` 句に指定された式からの値の任意の組み合わせが含まれる可能性があります。 `Into` 句の有効な式の詳細については、「[Aggregate 句](aggregate-clause.md)」を参照してください。  
  
 `Group Join` 操作では、`Group Join` 演算子の左側に指定されたコレクションからのすべての結果が返されます。 これは、結合されているコレクションに一致するものがない場合でも当てはまります。 これは、SQL の `LEFT OUTER JOIN` に似ています。  
  
 `Join` 句を使用して、コレクションを単一のコレクションに結合することができます。 これは、SQL の `INNER JOIN` と同じです。  
  
## <a name="example"></a>例  
 次のコード例では、`Group Join` 句を使用して 2 つのコレクションを結合しています。  
  
 [!code-vb[VbSimpleQuerySamples#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#14)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [Select 句](select-clause.md)
- [From 句](from-clause.md)
- [Join 句](join-clause.md)
- [WHERE 句](where-clause.md)
- [Group By 句](group-by-clause.md)
