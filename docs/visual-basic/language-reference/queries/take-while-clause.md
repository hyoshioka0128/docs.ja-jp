---
title: Take While 句
ms.date: 07/20/2015
f1_keywords:
- vb.QueryTakeWhile
helpviewer_keywords:
- queries [Visual Basic], Take While
- Take While clause [Visual Basic]
- Take While statement [Visual Basic]
ms.assetid: db8f9f2f-fc9f-4a6c-b0b8-1bf048147e11
ms.openlocfilehash: 4b6133efdbd9c46ab85201ad454671e5538b6a81
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359581"
---
# <a name="take-while-clause-visual-basic"></a>Take While 句 (Visual Basic)
指定された条件が `true` である限り、コレクションの要素を含むようにし、残りの要素をバイパスします。  
  
## <a name="syntax"></a>構文  
  
```vb  
Take While expression  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`expression`|必須です。 次の要素をテストするための条件を表す式。 式は、`Boolean` 値または同等の機能 (`Boolean` として評価される `Integer` など) を返す必要があります。|  
  
## <a name="remarks"></a>Remarks  
 `Take While` 句には、クエリ結果の先頭から、指定された `expression` で `false` が返されるまでの要素が含まれます。 `expression` が `false` を返すと、クエリでは残りのすべての要素がバイパスされます。 残りの結果に対して、`expression` は無視されます。  
  
 `Take While` 句は、`Where` 句を使用して、特定の条件を満たすクエリからのすべての要素を含めることができるという点で、`Where` 句と異なります。 `Take While` 句には、初めて条件が満たされなくなったときまでの要素が含まれます。 `Take While` 句は、順序付けされたクエリ結果を操作する場合に最も役立ちます。  
  
## <a name="example"></a>例  
 次のコード例では、`Take While` 句を使用して、注文がない最初の顧客が見つかるまで結果を取得します。  
  
 [!code-vb[VbSimpleQuerySamples#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [Select 句](select-clause.md)
- [From 句](from-clause.md)
- [Take 句](take-clause.md)
- [Skip While 句](skip-while-clause.md)
- [WHERE 句](where-clause.md)
