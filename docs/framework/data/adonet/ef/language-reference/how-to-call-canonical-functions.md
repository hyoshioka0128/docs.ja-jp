---
title: '方法: Canonical 関数を呼び出す'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b3d84873-7403-4957-8e20-b4ae39f50214
ms.openlocfilehash: a1c550b35142cffceeaf08f7d9ff049c766307e0
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70397561"
---
# <a name="how-to-call-canonical-functions"></a>方法: Canonical 関数を呼び出す
<xref:System.Data.Objects.EntityFunctions> クラスには、LINQ to Entities クエリで使用する正規関数を公開するメソッドが含まれています。 正規関数については、「[正規関数](canonical-functions.md)」を参照してください。  
  
> [!NOTE]
> <xref:System.Data.Objects.EntityFunctions.AsUnicode%2A> クラスの <xref:System.Data.Objects.EntityFunctions.AsNonUnicode%2A> メソッドと <xref:System.Data.Objects.EntityFunctions> メソッドには正規関数に相当するものがありません。  
  
 値のセットに対して計算を実行して 1 つの値を返す正規関数 (集計正規関数とも呼ばれる) は、直接呼び出すことができます。 他の正規関数は、LINQ to Entities クエリの一部としてしか呼び出すことができません。 集計関数を直接呼び出すには、その関数に <xref:System.Data.Objects.ObjectQuery%601> を渡す必要があります。 詳細については、以下の 2 番目の例を参照してください。  
  
 一部の正規関数は、LINQ to Entities クエリで共通言語ランタイム (CLR) メソッドを使用して呼び出すことができます。 正規関数にマップされる CLR メソッドの一覧については、「[CLR メソッドと正規関数とのマッピング](clr-method-to-canonical-function-mapping.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、[AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) を使用します。 この例で実行される LINQ to Entities クエリは、<xref:System.Data.Objects.EntityFunctions.DiffDays%2A> メソッドを使用して、`SellEndDate` と `SellStartDate` の差が 365 日よりも少ないすべての製品を返します。  
  
 [!code-csharp[DP L2E CanonicalAndStoreFunctions#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e canonicalandstorefunctions/cs/program.cs#1)]
 [!code-vb[DP L2E CanonicalAndStoreFunctions#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e canonicalandstorefunctions/vb/module1.vb#1)]  
  
## <a name="example"></a>例  
 次の例では、[AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) を使用します。 この例では、<xref:System.Data.Objects.EntityFunctions.StandardDeviation%2A> の小計の標準偏差を返す集計 `SalesOrderHeader` メソッドを直接呼び出します。 <xref:System.Data.Objects.ObjectQuery%601> は関数に渡されているため、LINQ to Entities クエリに含まれていなくても呼び出すことができる点に注意してください。  
  
 [!code-csharp[DP L2E CanonicalAndStoreFunctions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e canonicalandstorefunctions/cs/program.cs#2)]
 [!code-vb[DP L2E CanonicalAndStoreFunctions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e canonicalandstorefunctions/vb/module1.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [LINQ to Entities クエリ内の関数の呼び出し](calling-functions-in-linq-to-entities-queries.md)
- [LINQ to Entities でのクエリ](queries-in-linq-to-entities.md)
