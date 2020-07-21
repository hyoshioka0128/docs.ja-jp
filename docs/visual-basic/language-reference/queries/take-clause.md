---
title: Take 句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryTake
helpviewer_keywords:
- Take statement [Visual Basic]
- queries [Visual Basic], Take
- Take clause [Visual Basic]
ms.assetid: 77bf87b2-1476-4456-957f-fee922fbad8c
ms.openlocfilehash: 25dd06905525a96bc1504f033eb4f19af6d454a2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359633"
---
# <a name="take-clause-visual-basic"></a>Take 句 (Visual Basic)
コレクションの先頭から、指定された数の連続する要素を返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Take count  
```  
  
## <a name="parts"></a>指定項目  
 `count`  
 必須です。 返されるシーケンスの要素数に評価される値または式。  
  
## <a name="remarks"></a>Remarks  
 `Take` 句を指定すると、結果リストの先頭から指定した数の連続した要素がクエリに含まれます。 含まれる要素の数は `count` パラメーターによって指定します。  
  
 `Skip` 句と共に `Take` 句を使用すると、クエリの任意のセグメントからのデータの範囲を返すことができます。 これを行うには、範囲の最初の要素のインデックスを `Skip` 句に渡し、範囲のサイズを `Take` 句に渡します。 この場合、`Take` 句を `Skip` 句の後に指定する必要があります。  
  
 クエリで `Take` 句を使用する場合は、`Take` 句に目的の結果が含まれるようにする順番で、結果が返されるようにする必要がある場合もあります。 クエリ結果の順序付けの詳細については、「[Order By 句](order-by-clause.md)」を参照してください。  
  
 指定した条件に応じて、特定の要素のみが返されるように指定するには、`TakeWhile` 句を使用できます。  
  
## <a name="example"></a>例  
 次のコード例では、`Skip` 句と共に `Take` 句を使用して、ページ内のクエリからのデータを返しています。 GetCustomers 関数では、`Skip` 句を使用して、指定した開始インデックス値までリスト内の顧客をバイパスし、`Take` 句を使用して、そのインデックス値から始まる顧客のページを返します。  
  
 [!code-vb[VbSimpleQuerySamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [Select 句](select-clause.md)
- [From 句](from-clause.md)
- [Order By 句](order-by-clause.md)
- [Take While 句](take-while-clause.md)
- [Skip 句](skip-clause.md)
