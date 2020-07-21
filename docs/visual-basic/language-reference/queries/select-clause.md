---
title: Select 句
ms.date: 07/20/2015
f1_keywords:
- vb.QuerySelect
helpviewer_keywords:
- Select statement [Visual Basic]
- Select clause [Visual Basic]
- queries [Visual Basic], Select
ms.assetid: 27a3f61c-5960-4692-9b91-4d0c4b6178fe
ms.openlocfilehash: a909b1d79b10f82ece03bab788ae889c64b27124
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359695"
---
# <a name="select-clause-visual-basic"></a>Select 句 (Visual Basic)
クエリの結果を定義します。  
  
## <a name="syntax"></a>構文  
  
```vb  
Select [ var1 = ] fieldName1 [, [ var2 = ] fieldName2 [...] ]  
```  
  
## <a name="parts"></a>指定項目  
 `var1`  
 任意。 列式の結果を参照するために使用できる別名。  
  
 `fieldName1`  
 必須です。 クエリ結果に返されるフィールドの名前。  
  
## <a name="remarks"></a>Remarks  
 `Select` 句を使用して、クエリから返される結果を定義できます。 これにより、クエリによって作成された新しい匿名型のメンバーを定義することも、クエリによって返される名前付きの型のメンバーを対象にすることもできます。 `Select` 句は、クエリには必要ありません。 `Select` 句が指定されていない場合、クエリは、現在のスコープで識別される範囲変数のすべてのメンバーに基づいて型を返します。 詳細については、「[匿名型](../../programming-guide/language-features/objects-and-classes/anonymous-types.md)」を参照してください。 クエリで名前付きの型を作成すると、型 <xref:System.Collections.Generic.IEnumerable%601> の結果が返されます。ここで `T` は作成された型です。  
  
 `Select` 句は、現在のスコープ内の任意の変数を参照できます。 これには、`From` 句 (または `From` 句) で識別される範囲変数が含まれます。 また、`Aggregate`、`Let`、`Group By`、`Group Join` の各句による別名で作成された新しい変数、またはクエリ式の前の `Select` 句からの変数も含まれます。 また、`Select` 句には静的な値を含めることもできます。 たとえば、次のコード例は、`Select` 句で `ProductName`、`Price`、`Discount`、および `DiscountedPrice` の 4 つのメンバーを持つ新しい匿名型としてクエリ結果を定義するクエリ式を示しています。 `ProductName` メンバーと `Price` メンバーの値は、`From` 句で定義されている製品の範囲変数から取得されます。 `DiscountedPrice` メンバーの値は、`Let` 句で計算されます。 `Discount` メンバーは静的な値です。  
  
 [!code-vb[VbSimpleQuerySamples#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#27)]  
  
 `Select` 句には、後続のクエリ句の範囲変数の新しいセットが導入され、以前の範囲変数はスコープに含まれなくなりました。 クエリ式の最後の `Select` 句によって、クエリの戻り値が決まります。 たとえば、次のクエリでは、合計が 500 を超えるすべての顧客の注文の会社名と注文 ID が返されます。 最初の `Select` 句は、`Where` 句と 2 番目の `Select` 句の範囲変数を識別します。 2 番目の `Select` 句は、クエリによって返される値を新しい匿名型として識別します。  
  
 [!code-vb[VbSimpleQuerySamples#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#28)]  
  
 `Select` 句が返される項目を 1 つ識別する場合、クエリ式はその 1 つの項目の型のコレクションを返します。 `Select` 句が返される項目を複数識別する場合、クエリ式は、選択した項目に基づいて、新しい匿名型のコレクションを返します。 たとえば、次の 2 つのクエリは、`Select` 句に基づいて 2 つの異なる型のコレクションを返します。 最初のクエリは、会社名のコレクションを文字列として返します。 2 番目のクエリは、会社名と住所情報が入力された `Customer` オブジェクトのコレクションを返します。  
  
 [!code-vb[VbSimpleQuerySamples#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#29)]  
  
## <a name="example"></a>例  
 次のクエリ式では、`From` 句を使用して、`customers` コレクションに対して `cust` 範囲変数を宣言しています。 `Select` 句は、顧客名と ID 値を選択し、新しい範囲変数に対して `CompanyName` 列と `CustomerID` 列を設定します。 `For Each` ステートメントは、返された各オブジェクトをループし、各レコードの `CompanyName` 列と `CustomerID` 列を表示します。  
  
 [!code-vb[VbSimpleQuerySamples#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#30)]  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [クエリ](index.md)
- [From 句](from-clause.md)
- [WHERE 句](where-clause.md)
- [Order By 句](order-by-clause.md)
- [匿名型](../../programming-guide/language-features/objects-and-classes/anonymous-types.md)
