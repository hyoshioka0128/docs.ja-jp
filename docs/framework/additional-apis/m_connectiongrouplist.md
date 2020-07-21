---
title: ServicePoint. m_ConnectionGroupList フィールド
description: ServicePoint. m_ConnectionGroupList フィールドについて説明します。これは、各接続グループのハッシュテーブルであり、それぞれが .NET の ServicePoint URI の接続を保持します。
ms.date: 05/01/2017
topic_type:
- apiref
api_name:
- System.Net.ServicePoint.m_ConnectionGroupList
api_location:
- System.dll
api_type:
- Assembly
ms.assetid: df8afb59-f0f6-4ddc-b3c1-839b9fc601d8
ms.openlocfilehash: 0ebfeb782147f21abfde536b8053fa15b1e1a602
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989708"
---
# <a name="servicepointm_connectiongrouplist-field"></a>ServicePoint. m \_ connectiongrouplist フィールド

`ServicePoint.m_ConnectionGroupList`は、 <xref:System.Collections.Hashtable> それぞれの URI の接続を保持する接続グループのです <xref:System.Net.ServicePoint> 。

## <a name="syntax"></a>構文
  
```csharp  
private Hashtable m_ConnectionGroupList
```

> [!WARNING]
> `ServicePoint.m_ConnectionGroupList`フィールドはプライベートであり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのフィールドの使用はサポートしていません。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)

**.NET Framework のバージョン:** 2.0 以降で使用できます。
