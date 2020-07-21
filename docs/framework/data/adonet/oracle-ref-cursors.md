---
title: Oracle REF CURSOR
ms.date: 03/30/2017
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
ms.openlocfilehash: 7cd29a6a20015c7ce4475b0211cb07f7ee78b530
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794872"
---
# <a name="oracle-ref-cursors"></a>Oracle REF CURSOR
.NET Framework Data Provider for Oracle では、Oracle の **REF CURSOR** データ型がサポートされています。 データ プロバイダーを使用して Oracle REF CURSOR を操作するときは、次の動作を考慮する必要があります。  
  
> [!NOTE]
> 動作の中には、Microsoft OLE DB Provider for Oracle (MSDAORA) の動作と異なるものがあります。  
  
- パフォーマンスの理由から、Data Provider for Oracle では、バインドするよう明示的に指定した場合を除き、**REF CURSOR** データ型が自動的にバインドされることはありません。これは、MSDAORA の場合と同じです。  
  
- データ プロバイダーでは、REF CURSOR パラメーターの指定に使用する {resultset} エスケープのような、ODBC エスケープ シーケンスはサポートされていません。  
  
- REF CURSOR を返すストアド プロシージャを実行するには、<xref:System.Data.OracleClient.OracleParameterCollection> のパラメーターで、<xref:System.Data.OracleClient.OracleType> を **Cursor** に、<xref:System.Data.OracleClient.OracleParameter.Direction%2A> を **Output** に定義する必要があります。 データ プロバイダーでは、REF CURSOR のバインドは出力パラメーターとしてのみサポートされています。 プロバイダーは、入力パラメーターとしての REF CURSOR はサポートしていません。  
  
- パラメーター値からの <xref:System.Data.OracleClient.OracleDataReader> の取得はサポートされていません。 値は、コマンドを実行すると <xref:System.DBNull> 型になります。  
  
- REF CURSOR で動作する **CommandBehavior** 列挙値は (たとえば、<xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A> を呼び出すとき)、**CloseConnection** だけです。それ以外はすべて無視されます。  
  
- **OracleDataReader** 内の REF CURSOR の順序は、**OracleParameterCollection** でのパラメーターの順序によって決まります。 <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A> プロパティは無視されます。  
  
- PL/SQL の **TABLE** データ型はサポートされていません。 ただし、REF CURSOR は、さらに効果的です。 **TABLE** データ型を使用する必要がある場合は、MSDAORA と共に OLE DB .NET データ プロバイダーを使用します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [REF CURSOR の例](ref-cursor-examples.md)  
 次の 3 つの例を使って REF CURSOR の使い方について説明します。  
  
 [OracleDataReader の REF CURSOR パラメーター](ref-cursor-parameters-in-an-oracledatareader.md)  
 REF CURSOR パラメーターを返し、**OracleDataReader** として値を読み取る、PL/SQL のストアド プロシージャを実行する方法を示します。  
  
 [OracleDataReader を使用した複数の REF CURSOR からのデータの取得](retrieving-data-from-multiple-ref-cursors.md)  
 REF CURSOR パラメーターを返し、**OracleDataReader** を使用して値を読み取る、PL/SQL のストアド プロシージャを実行する方法を示します。  
  
 [1 つまたは複数の REF CURSOR を使用した DataSet の値の設定](filling-a-dataset-using-one-or-more-ref-cursors.md)  
 2 つの REF CURSOR パラメーターを返し、返された行を <xref:System.Data.DataSet> に入力する、PL/SQL ストアド プロシージャを実行する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [Oracle および ADO.NET](oracle-and-adonet.md)
- [ADO.NET の概要](ado-net-overview.md)
