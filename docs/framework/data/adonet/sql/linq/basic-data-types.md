---
title: 基本データ型
ms.date: 03/30/2017
ms.assetid: eca2c472-9548-4800-bd31-5d8d9f11752b
ms.openlocfilehash: e85adb928925bf161e6e2d6ef935a20606f8eb32
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248024"
---
# <a name="basic-data-types"></a>基本データ型
LINQ to SQL クエリは、Microsoft SQL Server で実行される前に Transact-SQL に変換されるため、 LINQ to SQL は、SQL Server が基本データ型に対してサポートするのと同じ組み込み機能の多くをサポートします。  
  
## <a name="casting"></a>キャスト  
 SQL Server 内に同様の有効な変換が存在する場合は、変換元の CLR 型から変換先の CLR 型への暗黙的または明示的なキャストが有効になります。 CLR キャストの詳細については、「[CType 関数 (Visual Basic)](../../../../../visual-basic/language-reference/functions/ctype-function.md)」および[型のテストとキャストの演算子](../../../../../csharp/language-reference/operators/type-testing-and-cast.md)に関する記事を参照してください。 変換後、CLR 式に対して実行される操作の動作は、変換先の型に通常割り当てられる他の CLR 式の動作と一致するように、キャストによって変更されます。 継承の割り当てのコンテキストにおいてもキャストは変換可能です。 より厳密なエンティティ サブタイプにオブジェクトを変換して、そのサブタイプに固有のデータへのアクセスを可能にすることができます。  
  
## <a name="equality-operators"></a>等値演算子  
 LINQ to SQL は、LINQ to SQL クエリ内の基本データ型で次の等値演算子をサポートします。  
  
- 等値演算子および非等値演算子:等値演算子および非等値演算子は、数値型、<xref:System.Boolean> 型、<xref:System.DateTime> 型、および <xref:System.TimeSpan> 型についてサポートされます。 Visual Basic 演算子 `=` と `<>` の詳細については、「[比較演算子](../../../../../visual-basic/language-reference/operators/comparison-operators.md)」を参照してください。 C# の比較演算子 `==` および `!=` の詳細については、「[等値演算子](../../../../../csharp/language-reference/operators/equality-operators.md)」を参照してください。
  
- Is 演算子:`IS` 演算子には、継承の割り当ての使用時にサポートされる変換があります。 これは、オブジェクトが特定の種類のエンティティであるかどうかを検査する場合に、判別列を直接調べる代わりとして使用でき、判別列のチェックに変換されます。 Visual Basic と C# の Is 演算子の詳細については、「[Is 演算子](../../../../../visual-basic/language-reference/operators/is-operator.md)」および [is](../../../../../csharp/language-reference/operators/type-testing-and-cast.md#is-operator) に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目

- [SQL と CLR の型マッピング](sql-clr-type-mapping.md)
- [データ型と関数](data-types-and-functions.md)
