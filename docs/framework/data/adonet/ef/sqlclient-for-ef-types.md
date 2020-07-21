---
title: Entity Framework 用 SqlClient の型
ms.date: 03/30/2017
ms.assetid: f2a95ead-c845-4e97-9fb3-04b444f7ed81
ms.openlocfilehash: d132583bba2520d37693be6c4b085cfa514003e0
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73737845"
---
# <a name="sqlclient-for-entity-frameworktypes"></a>Entity Framework 用 SqlClient の型
.NET Framework Data Provider for SQL Server (SqlClient) プロバイダー マニフェスト ファイルには、プロバイダー プリミティブ型のリスト、それぞれの型のファセット、概念モデルとストレージ モデルのプリミティブ型とのマッピング、および概念モデルとストレージ モデルのプリミティブ型間での昇格と変換の規則が含まれています。  
  
 次の表では、SQL Server 2008、SQL Server 2005、SQL Server 2000 データベースの型と、これらの型が概念モデル型にどのようにマップされるかを示します。 いくつかの新しい型が SQL Server の新しいバージョンで導入されており、これらの型は SQL Server の古いバージョンではサポートされていません。 これらの型については次の表で説明します。  
  
|プロバイダー型の<br /><br /> name|プロバイダー型の<br /><br /> 属性|`EDMSimpleType`<br /><br /> name|ファセット|  
|----------------------------|----------------------------------|------------------------------|------------|  
|`bit`|N/A|`Edm.Boolean`|N/A|  
|`tinyint`|N/A|`Edm.Byte`|N/A|  
|`smallint`|N/A|`Edm.Int16`|N/A|  
|`int`|N/A|`Edm.Int32`|N/A|  
|`bigint`|N/A|`Edm.Int64`|N/A|  
|`float`|N/A|`Edm.Double`|N/A|  
|`real`|N/A|`Edm.Double`|N/A|  
|`decimal`|N/A|`Edm.Decimal`|精度:<br /><br /> - 最小値: 1<br /><br /> - 最大値:38<br /><br /> - 既定:18<br /><br /> - 定数: False<br /><br /> スケール:<br /><br /> - 最小値: 0<br /><br /> - 最大値:38<br /><br /> - 既定:0<br /><br /> - 定数: False|  
|`numeric`|N/A|`Edm.Decimal`|精度:<br /><br /> - 最小値: 1<br /><br /> - 最大値:38<br /><br /> - 既定:18<br /><br /> - 定数: False<br /><br /> スケール:<br /><br /> - 最小値: 0<br /><br /> - 最大値:38<br /><br /> - 既定:0<br /><br /> - 定数: False|  
|`smallmoney`|N/A|`Edm.Decimal`|精度:<br /><br /> - 既定:10<br /><br /> - 定数: True<br /><br /> スケール:<br /><br /> - 既定:4<br /><br /> - 定数: True|  
|`money`|N/A|`Edm.Decimal`|精度:<br /><br /> - 既定:19<br /><br /> - 定数: True<br /><br /> スケール:<br /><br /> - 既定:4<br /><br /> - 定数: True|  
|`binary`|N/A|`Edm.Binary`|MaxLength:<br /><br /> - 最小値: 1<br /><br /> - 最大値:8000<br /><br /> - 既定:8000<br /><br /> - 定数: False<br /><br /> FixedLength:<br /><br /> - 既定:True<br /><br /> - 定数: True|  
|`varbinary`|N/A|`Edm.Binary`|MaxLength:<br /><br /> - 最小値: 1<br /><br /> - 最大値:8000<br /><br /> - 既定:8000<br /><br /> - 定数: False<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`varbinary(max)`<br /><br /> メモ:この型は、SQL Server 2000 ではサポートされていません。|N/A|`Edm.Binary`|MaxLength:<br /><br /> - 既定:214748364780<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`image`|N/A|`Edm.Binary`|MaxLength:<br /><br /> - 既定:2147483647<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`timestamp`|N/A|`Edm.Binary`|MaxLength:<br /><br /> - 既定:8<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:True<br /><br /> - 定数: True|  
|`rowversion`|N/A|`Edm.Binary`|MaxLength:<br /><br /> - 既定:8<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:True<br /><br /> - 定数: True|  
|`smalldatetime`|N/A|`Edm.DateTime`|精度:<br /><br /> - 既定:0<br /><br /> - 定数: True|  
|`datetime`|N/A|`Edm.DateTime`|精度:<br /><br /> - 既定:3<br /><br /> - 定数: True|  
|`date`<br /><br /> メモ:この型は、SQL Server 2005 と SQL Server 2000 ではサポートされていません。|N/A|`Edm.DateTime`|精度:<br /><br /> - 既定:0<br /><br /> - 定数: False|  
|`time`<br /><br /> メモ:この型は、SQL Server 2005 と SQL Server 2000 ではサポートされていません。|N/A|`Edm.Time`|精度:<br /><br /> - 既定:7<br /><br /> - 定数: False|  
|`datetime2`<br /><br /> メモ:この型は、SQL Server 2005 と SQL Server 2000 ではサポートされていません。|N/A|`Edm.DateTime`|精度:<br /><br /> - 既定:7<br /><br /> - 定数: False|  
|`datetimeoffset`<br /><br /> メモ:この型は、SQL Server 2005 と SQL Server 2000 ではサポートされていません。|N/A|`Edm.DateTimeOffset`|精度:<br /><br /> - 既定:7<br /><br /> - 定数: False|  
|`nvarchar`<br /><br /> メモ:この型は、SQL Server 2000 ではサポートされていません。|N/A|`Edm.String`|MaxLength:<br /><br /> - 最小値: 1<br /><br /> - 最大値:4000<br /><br /> - 既定:4000<br /><br /> - 定数: False<br /><br /> Unicode: <br /><br /> - 既定:True<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`varchar`<br /><br /> メモ:この型は、SQL Server 2000 ではサポートされていません。|N/A|`Edm.String`|MaxLength:<br /><br /> - 最小値: 1<br /><br /> - 最大値:8000<br /><br /> - 既定:8000<br /><br /> - 定数: False<br /><br /> Unicode: <br /><br /> - 既定:False<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`char`|N/A|`Edm.String`|MaxLength:<br /><br /> - 最小値: 1<br /><br /> - 最大値:8000<br /><br /> - 既定:8000<br /><br /> - 定数: False<br /><br /> Unicode: <br /><br /> - 既定:False<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:True<br /><br /> - 定数: True|  
|`nchar`|N/A|`Edm.String`|MaxLength:<br /><br /> - 最小値: 1<br /><br /> - 最大値:4000<br /><br /> - 既定:4000<br /><br /> - 定数: False<br /><br /> Unicode: <br /><br /> - 既定:True<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:True<br /><br /> - 定数: True|  
|`varchar`(`max`)|N/A|`Edm.String`|MaxLength:<br /><br /> - 既定:2147483647<br /><br /> - 定数: True<br /><br /> Unicode: <br /><br /> - 既定:False<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`nvarchar`(`max`)|N/A|`Edm.String`|MaxLength:<br /><br /> - 既定:1073741823<br /><br /> - 定数: True<br /><br /> Unicode: <br /><br /> - 既定:True<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`ntext`|等値比較可能:False<br /><br /> 順序比較可能:False|`Edm.String`|MaxLength:<br /><br /> - 既定:1073741823<br /><br /> - 定数: True<br /><br /> Unicode: <br /><br /> - 既定:False<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`text`|等値比較可能:False<br /><br /> 順序比較可能:False|`Edm.String`|MaxLength:<br /><br /> - 既定:2147483647<br /><br /> - 定数: True<br /><br /> Unicode: <br /><br /> - 既定:False<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
|`Unique`<br /><br /> `identifier`|等値比較可能:True<br /><br /> 順序比較可能:True|`Edm.Guid`|N/A|  
|`xml`|等値比較可能:False<br /><br /> 順序比較可能:False|`Edm.String`|MaxLength:<br /><br /> - 既定:1073741823<br /><br /> - 定数: True<br /><br /> Unicode: <br /><br /> - 既定:True<br /><br /> - 定数: True<br /><br /> FixedLength:<br /><br /> - 既定:False<br /><br /> - 定数: True|  
  
## <a name="see-also"></a>関連項目

- [CSDL、SSDL、および MSL 仕様](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
