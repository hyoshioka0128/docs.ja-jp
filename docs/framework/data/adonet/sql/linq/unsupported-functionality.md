---
title: サポートされていない機能
ms.date: 03/30/2017
ms.assetid: e480cfb5-697e-42c8-bed5-9264c945c4f9
ms.openlocfilehash: fb030a5f212be71d99b66f101e5e8411fbe4de33
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64618138"
---
# <a name="unsupported-functionality"></a>サポートされていない機能
LINQ to SQL では、次の SQL 機能は、既存の共通言語ランタイム (CLR) および .NET Framework の構成要素の変換からは公開できません。  
  
- `STDDEV`  
  
- `LIKE`  
  
     `LIKE` は直接変換によってサポートされませんが、同様の機能が <xref:System.Data.Linq.SqlClient.SqlMethods> クラスにあります。 詳細については、「<xref:System.Data.Linq.SqlClient.SqlMethods.Like%2A?displayProperty=nameWithType>」を参照してください。  
  
- `DATEDIFF`  
  
     LINQ to SQL では、`DATEDIFF` のサポートが制限されています。 同様の機能が <xref:System.Data.Linq.SqlClient.SqlMethods> クラスにあります。  
  
- `ROUND`  
  
     LINQ to SQL では、`ROUND` のサポートが制限されています。 詳細については、「[System.Math メソッド](system-math-methods.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [データ型と関数](data-types-and-functions.md)
