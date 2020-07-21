---
title: SQL XML 列値
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.openlocfilehash: 03b09d3a53c725bb0e84ba6b5d98944267bc564c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780792"
---
# <a name="sql-xml-column-values"></a>SQL XML 列値
SQL Server では、`xml` データ型をサポートしています。開発者は、<xref:System.Data.SqlClient.SqlCommand> クラスの標準動作を使用し、この型を含む結果セットを取得できます。 任意の列が (<xref:System.Data.SqlClient.SqlDataReader> などに) 取得されるように、`xml` 列を取得できますが、列のコンテンツを XML として操作する必要がある場合は、<xref:System.Xml.XmlReader> を使用する必要があります。  
  
## <a name="example"></a>例  
 次のコンソール アプリケーションでは、**AdventureWorks** データベースの **Sales.Store** テーブルから 2 行を選択し、この行の `xml` 列を <xref:System.Data.SqlClient.SqlDataReader> インスタンスに格納します。 行ごとに、<xref:System.Data.SqlClient.SqlDataReader> の <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> メソッドを使用して `xml` 列の値が読み取られます。 この値は <xref:System.Xml.XmlReader> に格納されます。 コンテンツを <xref:System.Data.SqlTypes.SqlXml> 変数に設定する場合は、<xref:System.Data.IDataRecord.GetValue%2A> メソッドではなく <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> を使用する必要があることに注意してください。<xref:System.Data.IDataRecord.GetValue%2A> は、`xml` 列の値を文字列として返します。  
  
> [!NOTE]
> **AdventureWorks** サンプル データベースは、既定では SQL Server のインストール時にはインストールされません。 SQL Server Setup を実行してインストールします。  
  
 [!code-csharp[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.SqlTypes.SqlXml>
- [SQL Server における XML データ](xml-data-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
