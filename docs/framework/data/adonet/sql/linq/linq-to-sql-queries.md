---
title: LINQ to SQL クエリ
ms.date: 03/30/2017
ms.assetid: f4897aaa-7f44-4c20-a471-b948c2971aae
ms.openlocfilehash: 478138d26d6cdf656b2487c637a5eb13784126e9
ms.sourcegitcommit: 7bc6887ab658550baa78f1520ea735838249345e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75634381"
---
# <a name="linq-to-sql-queries"></a>LINQ to SQL クエリ
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のクエリは、LINQ と同じ構文を使用して定義します。 異なる点は、クエリ内で参照されるオブジェクトがデータベース内の要素に割り当てられるという点だけです。 詳細については、「[LINQ クエリの概要 (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)」を参照してください。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、作成したクエリを同等の SQL クエリに変換し、それをサーバーに送って処理します。 具体的には、アプリケーションは [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] API を使用してクエリの実行を要求します。 次に、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] プロバイダーがクエリを SQL テキストに変換し、ADO プロバイダーに実行を委任します。 ADO プロバイダーは、クエリの結果を `DataReader` として返します。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] プロバイダーにより、ADO の結果がユーザー オブジェクトの <xref:System.Linq.IQueryable> コレクションに変換されます。  
  
> [!NOTE]
> .NET Framework の組み込み型に対するほとんどのメソッドと演算子には、SQL に直接対応する変換が用意されています。 LINQ で変換できないものについては、ランタイム例外が発生します。 詳しくは、「[SQL と CLR の型マッピング](sql-clr-type-mapping.md)」をご覧ください。  
  
 次の表では、LINQ と [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のクエリ項目の類似点と相違点を示します。  
  
|アイテム|LINQ クエリ|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] クエリ|  
|----------|----------------|----------------------------------------------------------------------|  
|クエリを保持するローカル変数の戻り値の型 (シーケンスを返すクエリの場合)|ジェネリック `IEnumerable`|ジェネリック `IQueryable`|  
|データ ソースの指定|`From` 句 (Visual Basic) または `from` 句 (C#) を使用します。|同|  
|フィルター処理|`Where`/`where` 句を使用します|同|  
|グループ化|`Group…By`/`groupby` 句を使用します|同|  
|選択 (投影)|`Select`/`select` 句を使用します|同|  
|遅延実行と即時実行|「[LINQ クエリの概要 (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)」をご覧ください|同|  
|結合の実装|`Join`/`join` 句を使用します|`Join`/`join` 句を使用できますが、<xref:System.Data.Linq.Mapping.AssociationAttribute> 属性を使用する方が効果的です。 詳しくは、「[リレーションシップを介したクエリの実行](querying-across-relationships.md)」をご覧ください。|  
|リモート実行とローカル実行||詳しくは、「[リモート実行とローカル実行](remote-vs-local-execution.md)」をご覧ください。|  
|ストリーミングとキャッシュ クエリ|ローカル メモリ シナリオでは適用なし||  
  
## <a name="see-also"></a>関連項目

- [LINQ クエリの概要 (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)
- [LINQ クエリの基本操作](../../../../../csharp/programming-guide/concepts/linq/basic-linq-query-operations.md)
- [LINQ クエリ操作での型の関係](../../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)
- [クエリの概念](query-concepts.md)
