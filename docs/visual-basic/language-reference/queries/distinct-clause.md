---
title: Distinct 句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryDistinct
helpviewer_keywords:
- Distinct clause [Visual Basic]
- Distinct statement [Visual Basic]
- queries [Visual Basic], Distinct
ms.assetid: 86f42614-0d8f-4ffc-b888-ce8a37a8d36a
ms.openlocfilehash: 5aecffbce036500d294d03a925798d51f1269af6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401395"
---
# <a name="distinct-clause-visual-basic"></a>Distinct 句 (Visual Basic)
現在の範囲変数の値を制限して、後続のクエリ結果内で重複する値を除去します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Distinct  
```  
  
## <a name="remarks"></a>Remarks  
 `Distinct` 句を使用して、一意の項目の一覧を返すことができます。 `Distinct` 句によって、クエリで重複するクエリ結果を無視させます。 `Distinct` 句は、`Select` 句で指定されたすべての戻りフィールドの重複する値に適用されます。 `Select` 句が指定されていない場合、`Distinct` 句は `From` 句で識別されたクエリの範囲変数に適用されます。 範囲変数が変更できない型である場合、クエリでは、その型のすべてのメンバーが既存のクエリの結果と一致する場合にのみ、クエリの結果が無視されます。  
  
## <a name="example"></a>例  
 次のクエリ式では、顧客の一覧と顧客の注文の一覧が結合されます。 一意の顧客名と注文日の一覧を返すために、`Distinct` 句が含まれています。  
  
 [!code-vb[VbSimpleQuerySamples#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#20)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [From 句](from-clause.md)
- [Select 句](select-clause.md)
- [WHERE 句](where-clause.md)
