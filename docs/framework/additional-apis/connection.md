---
title: Connection クラス (System.Net)
ms.date: 05/01/2017
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Connection
api_location:
- System.dll
api_type:
- Assembly
ms.assetid: 6f0b8902-f31c-4ab9-a8c9-de43228995ec
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b3045e9f6a4b3d86580ec3bc5719520fed7d3a35
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74429351"
---
# <a name="connection-class"></a>Connection クラス

`Connection` クラスは、サーバーの応答、キューの要求、およびパイプライン要求を解析します。

## <a name="syntax"></a>構文
  
```csharp  
internal class Connection : PooledStream
```

> [!WARNING]
> `Connection` クラスは内部であり、コードで直接使用するためのものではありません。
> 
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="requirements"></a>要件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (.dll 内)

**.NET Framework のバージョン:** 2.0 以降で使用できます。
