---
title: ServicePointManager. CloseConnectionGroups メソッド (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.ServicePointManager.CloseConnectionGroups
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: aae9a389ae35e249d43c9dc830a68ec32cf4afef
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990535"
---
# <a name="servicepointmanagercloseconnectiongroups-method"></a>ServicePointManager. CloseConnectionGroups メソッド

すべてのサービスポイントを反復処理し、指定された名前の接続グループを閉じます。

```csharp
internal static void CloseConnectionGroups(string connectionGroupName)
```

> [!WARNING]
> このメソッドは内部であり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでこの方法を使用することはサポートしていません。

## <a name="parameters"></a>パラメーター

`connectionGroupName` <xref:System.String>

閉じる接続グループの名前。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
