---
title: OLE DB スキーマ コレクション
ms.date: 03/30/2017
ms.assetid: 6380c36b-658e-4d67-91e8-7131ef4a7c2c
ms.openlocfilehash: 2d5718c12100ebea49a6b6fab29a3790918c6ad3
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783450"
---
# <a name="ole-db-schema-collections"></a>OLE DB スキーマ コレクション
ここでは、Microsoft SQL Server、Oracle、および Microsoft Jet 用の各 OLE DB プロバイダーでのスキーマ コレクションのサポートについて説明します。  
  
## <a name="microsoft-sql-server-ole-db-provider"></a>Microsoft SQL Server OLE DB Provider  
 Microsoft SQL Server OLE DB Driver では、共通のスキーマ コレクションに加えて、次の特定のスキーマ コレクションがサポートされています。  
  
- [テーブル]  
  
- 列  
  
- プロシージャ  
  
- ProcedureParameters  
  
- Catalog  
  
- Indexes  
  
### <a name="tables"></a>[テーブル]  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|TABLE_TYPE|String|  
|TABLE_GUID|GUID|  
|DESCRIPTION|String|  
|TABLE_PROPID|Int64|  
|DATE_CREATED|DateTime|  
|DATE_MODIFIED|DateTime|  
  
### <a name="columns"></a>列  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|COLUMN_NAME|String|  
|COLUMN_GUID|GUID|  
|COLUMN_PROPID|Int64|  
|ORDINAL_POSITION|Int64|  
|COLUMN_HASDEFAULT|ブール型|  
|COLUMN_DEFAULT|String|  
|COLUMN_FLAGS|Int64|  
|IS_NULLABLE|ブール型|  
|DATA_TYPE|Int32|  
|TYPE_GUID|GUID|  
|CHARACTER_MAXIMUM_LENGTH|Int64|  
|CHARACTER_OCTET_LENGTH|Int64|  
|NUMERIC_PRECISION|Int32|  
|NUMERIC_SCALE|Int16|  
|DATETIME_PRECISION|Int64|  
|CHARACTER_SET_CATALOG|String|  
|CHARACTER_SET_SCHEMA|String|  
|CHARACTER_SET_NAME|String|  
|COLLATION_CATALOG|String|  
|COLLATION_SCHEMA|String|  
|COLLATION_NAME|String|  
|DOMAIN_CATALOG|String|  
|DOMAIN_SCHEMA|String|  
|DOMAIN_NAME|String|  
|DESCRIPTION|String|  
|COLUMN_LCID|Int32|  
|COLUMN_COMPFLAGS|Int32|  
|COLUMN_SORTID|Int32|  
|COLUMN_TDSCOLLATION|Byte[]|  
|IS_COMPUTED|ブール型|  
  
### <a name="procedures"></a>プロシージャ  
  
|ColumnName|DataType|  
|----------------|--------------|  
|PROCEDURE_CATALOG|String|  
|PROCEDURE_SCHEMA|String|  
|PROCEDURE_NAME|String|  
|PROCEDURE_TYPE|Int16|  
|PROCEDURE_DEFINITION|String|  
|DESCRIPTION|String|  
|DATE_CREATED|DateTime|  
|DATE_MODIFIED|DateTime|  
  
### <a name="procedureparameters"></a>ProcedureParameters  
  
|ColumnName|DataType|  
|----------------|--------------|  
|PROCEDURE_CATALOG|String|  
|PROCEDURE_SCHEMA|String|  
|PROCEDURE_NAME|String|  
|PARAMETER_NAME|String|  
|ORDINAL_POSITION|Int32|  
|PARAMETER_TYPE|Int32|  
|PARAMETER_HASDEFAULT|ブール型|  
|PARAMETER_DEFAULT|String|  
|IS_NULLABLE|ブール型|  
|DATA_TYPE|Int32|  
|CHARACTER_MAXIMUM_LENGTH|Int64|  
|CHARACTER_OCTET_LENGTH|Int64|  
|NUMERIC_PRECISION|Int32|  
|NUMERIC_SCALE|Int16|  
|DESCRIPTION|String|  
|TYPE_NAME|String|  
|LOCAL_TYPE_NAME|String|  
  
### <a name="catalog"></a>Catalog  
  
|ColumnName|DataType|  
|----------------|--------------|  
|CATALOG_NAME|String|  
|DESCRIPTION|String|  
  
### <a name="indexes"></a>Indexes  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|INDEX_CATALOG|String|  
|INDEX_SCHEMA|String|  
|INDEX_NAME|String|  
|PRIMARY_KEY|ブール型|  
|UNIQUE|ブール型|  
|CLUSTERED|ブール型|  
|TYPE|Int32|  
|FILL_FACTOR|Int32|  
|INITIAL_SIZE|Int32|  
|NULLS|Int32|  
|SORT_BOOKMARKS|ブール型|  
|AUTO_UPDATE|ブール型|  
|NULL_COLLATION|Int32|  
|ORDINAL_POSITION|Int64|  
|COLUMN_NAME|String|  
|COLUMN_GUID|GUID|  
|COLUMN_PROPID|Int64|  
|COLLATION|Int16|  
|CARDINALITY|Decimal (10 進数型)|  
|PAGES|Int32|  
|FILTER_CONDITION|String|  
|INTEGRATED|ブール型|  
  
## <a name="microsoft-oracle-ole-db-provider"></a>Microsoft Oracle OLE DB Provider  
 Microsoft Oracle OLE DB Driver は、共通のスキーマ コレクションに加えて次のスキーマ コレクションをサポートしています。  
  
- [テーブル]  
  
- 列  
  
- プロシージャ  
  
- ProcedureColumns  
  
- ProcedureParameters  
  
- Views  
  
- Indexes  
  
### <a name="tables"></a>[テーブル]  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|TABLE_TYPE|String|  
|TABLE_GUID|GUID|  
|DESCRIPTION|String|  
|TABLE_PROPID|Int64|  
|DATE_CREATED|DateTime|  
|DATE_MODIFIED|DateTime|  
  
### <a name="columns"></a>列  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|COLUMN_NAME|String|  
|COLUMN_GUID|GUID|  
|COLUMN_PROPID|Int64|  
|ORDINAL_POSITION|Int64|  
|COLUMN_HASDEFAULT|ブール型|  
|COLUMN_DEFAULT|String|  
|COLUMN_FLAGS|Int64|  
|IS_NULLABLE|ブール型|  
|DATA_TYPE|Int32|  
|TYPE_GUID|GUID|  
|CHARACTER_MAXIMUM_LENGTH|Int64|  
|CHARACTER_OCTET_LENGTH|Int64|  
|NUMERIC_PRECISION|Int32|  
|NUMERIC_SCALE|Int16|  
|DATETIME_PRECISION|Int64|  
|CHARACTER_SET_CATALOG|String|  
|CHARACTER_SET_SCHEMA|String|  
|CHARACTER_SET_NAME|String|  
|COLLATION_CATALOG|String|  
|COLLATION_SCHEMA|String|  
|COLLATION_NAME|String|  
|DOMAIN_CATALOG|String|  
|DOMAIN_SCHEMA|String|  
|DOMAIN_NAME|String|  
|DESCRIPTION|String|  
  
### <a name="procedures"></a>プロシージャ  
  
|ColumnName|DataType|  
|----------------|--------------|  
|PROCEDURE_CATALOG|String|  
|PROCEDURE_SCHEMA|String|  
|PROCEDURE_NAME|String|  
|PROCEDURE_TYPE|Int16|  
|PROCEDURE_DEFINITION|String|  
|DESCRIPTION|String|  
|DATE_CREATED|DateTime|  
|DATE_MODIFIED|DateTime|  
  
### <a name="procedurecolumns"></a>ProcedureColumns  
  
|ColumnName|DataType|  
|----------------|--------------|  
|PROCEDURE_CATALOG|String|  
|PROCEDURE_SCHEMA|String|  
|PROCEDURE_NAME|String|  
|COLUMN_NAME|String|  
|COLUMN_GUID|GUID|  
|COLUMN_PROPID|Int64|  
|ROWSET_NUMBER|Int64|  
|ORDINAL_POSITION|Int64|  
|IS_NULLABLE|ブール型|  
|DATA_TYPE|Int32|  
|TYPE_GUID|GUID|  
|CHARACTER_MAXIMUM_LENGTH|Int64|  
|CHARACTER_OCTET_LENGTH|Int64|  
|NUMERIC_PRECISION|Int32|  
|NUMERIC_SCALE|Int16|  
|DESCRIPTION|String|  
|OVERLOAD|Int16|  
  
### <a name="views"></a>Views  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|VIEW_DEFINITION|String|  
|CHECK_OPTION|ブール型|  
|IS_UPDATABLE|ブール型|  
|DESCRIPTION|String|  
|DATE_CREATED|DateTime|  
|DATE_MODIFIED|DateTime|  
  
### <a name="indexes"></a>Indexes  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|INDEX_CATALOG|String|  
|INDEX_SCHEMA|String|  
|INDEX_NAME|String|  
|PRIMARY_KEY|ブール型|  
|UNIQUE|ブール型|  
|CLUSTERED|ブール型|  
|TYPE|Int32|  
|FILL_FACTOR|Int32|  
|INITIAL_SIZE|Int32|  
|NULLS|Int32|  
|SORT_BOOKMARKS|ブール型|  
|AUTO_UPDATE|ブール型|  
|NULL_COLLATION|Int32|  
|ORDINAL_POSITION|Int64|  
|COLUMN_NAME|String|  
|COLUMN_GUID|GUID|  
|COLUMN_PROPID|Int64|  
|COLLATION|Int16|  
|CARDINALITY|Decimal (10 進数型)|  
|PAGES|Int32|  
|FILTER_CONDITION|String|  
|INTEGRATED|ブール型|  
  
## <a name="microsoft-jet-ole-db-provider"></a>Microsoft Jet OLE DB Provider  
 Microsoft Jet OLE DB Driver は、共通のスキーマ コレクションに加えて次のスキーマ コレクションをサポートしています。  
  
- [テーブル]  
  
- 列  
  
- プロシージャ  
  
- Views  
  
- Indexes  
  
### <a name="tables"></a>[テーブル]  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|TABLE_TYPE|String|  
|TABLE_GUID|GUID|  
|DESCRIPTION|String|  
|TABLE_PROPID|Int64|  
|DATE_CREATED|DateTime|  
|DATE_MODIFIED|DateTime|  
  
### <a name="columns"></a>列  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|COLUMN_NAME|String|  
|COLUMN_GUID|GUID|  
|COLUMN_PROPID|Int64|  
|ORDINAL_POSITION|Int64|  
|COLUMN_HASDEFAULT|ブール型|  
|COLUMN_DEFAULT|String|  
|COLUMN_FLAGS|Int64|  
|IS_NULLABLE|ブール型|  
|DATA_TYPE|Int32|  
|TYPE_GUID|GUID|  
|CHARACTER_MAXIMUM_LENGTH|Int64|  
|CHARACTER_OCTET_LENGTH|Int64|  
|NUMERIC_PRECISION|Int32|  
|NUMERIC_SCALE|Int16|  
|DATETIME_PRECISION|Int64|  
|CHARACTER_SET_CATALOG|String|  
|CHARACTER_SET_SCHEMA|String|  
|CHARACTER_SET_NAME|String|  
|COLLATION_CATALOG|String|  
|COLLATION_SCHEMA|String|  
|COLLATION_NAME|String|  
|DOMAIN_CATALOG|String|  
|DOMAIN_SCHEMA|String|  
|DOMAIN_NAME|String|  
|DESCRIPTION|String|  
  
### <a name="procedures"></a>プロシージャ  
  
|ColumnName|DataType|  
|----------------|--------------|  
|PROCEDURE_CATALOG|String|  
|PROCEDURE_SCHEMA|String|  
|PROCEDURE_NAME|String|  
|PROCEDURE_TYPE|Int16|  
|PROCEDURE_DEFINITION|String|  
|DESCRIPTION|String|  
|DATE_CREATED|DateTime|  
|DATE_MODIFIED|DateTime|  
  
### <a name="views"></a>Views  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|VIEW_DEFINITION|String|  
|CHECK_OPTION|ブール型|  
|IS_UPDATABLE|ブール型|  
|DESCRIPTION|String|  
|DATE_CREATED|DateTime|  
|DATE_MODIFIED|DateTime|  
  
### <a name="indexes"></a>Indexes  
  
|ColumnName|DataType|  
|----------------|--------------|  
|TABLE_CATALOG|String|  
|TABLE_SCHEMA|String|  
|TABLE_NAME|String|  
|INDEX_CATALOG|String|  
|INDEX_SCHEMA|String|  
|INDEX_NAME|String|  
|PRIMARY_KEY|ブール型|  
|UNIQUE|ブール型|  
|CLUSTERED|ブール型|  
|TYPE|Int32|  
|FILL_FACTOR|Int32|  
|INITIAL_SIZE|Int32|  
|NULLS|Int32|  
|SORT_BOOKMARKS|ブール型|  
|AUTO_UPDATE|ブール型|  
|NULL_COLLATION|Int32|  
|ORDINAL_POSITION|Int64|  
|COLUMN_NAME|String|  
|COLUMN_GUID|GUID|  
|COLUMN_PROPID|Int64|  
|COLLATION|Int16|  
|CARDINALITY|Decimal (10 進数型)|  
|PAGES|Int32|  
|FILTER_CONDITION|String|  
|INTEGRATED|ブール型|  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](ado-net-overview.md)
