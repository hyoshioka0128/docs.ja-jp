---
title: 関数 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 52b3d776-5acc-4f69-b614-5a43ce56ef9f
ms.openlocfilehash: ec94a0f16fb3b836297f6675cc938a711816555b
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250916"
---
# <a name="functions-entity-sql"></a>関数 (Entity SQL)
Entity SQL では、ユーザー定義関数、正規の関数、およびプロバイダー固有の関数がサポートされています。 ユーザー定義関数は、概念モデルまたはクエリでインラインで指定されます。 詳しくは、「[ユーザー定義関数](user-defined-functions-entity-sql.md)」をご覧ください。  
  
 正規の関数は Entity Framework で定義済みであり、データ プロバイダーによってサポートされています。 プロバイダーによってサポートされていない関数を呼び出すと、Entity SQL コマンドは失敗します。 そのため、通常は、プロバイダー固有の名前空間にあるストア固有の関数よりも正規の関数が推奨されます。 詳しくは、「[正規関数](canonical-functions.md)」をご覧ください。  
  
 Microsoft SQL クライアント マネージド プロバイダーは、プロバイダー固有の一連の関数を提供しています。 詳細については、「[Entity Framework 用 SqlClient 関数](../sqlclient-for-ef-functions.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ユーザー定義関数](user-defined-functions-entity-sql.md)  
  
 [関数のオーバーロードの解決方法](function-overload-resolution-entity-sql.md)  
  
 [集計関数](../aggregate-functions-sqlclient-for-entity-framework.md)  
  
## <a name="see-also"></a>関連項目

- [Entity SQL の概要](entity-sql-overview.md)
