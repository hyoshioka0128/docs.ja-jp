---
title: HttpStatusDescription クラス (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.HttpStatusDescription
- System.Net.HttpStatusDescription.Get
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 0214d8259c735de11abe204680d619a7298466de
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990543"
---
# <a name="httpstatusdescription-class"></a>HttpStatusDescription クラス

標準の HTTP 状態の説明を提供します。 このクラスは継承できません。

```csharp
internal static class HttpStatusDescription
```

> [!WARNING]
> このクラスは内部的なものであり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="get-method"></a>Get メソッド

指定された HTTP ステータスコードに関連付けられている説明を返します。

```csharp
internal static string Get(int code)
```

### <a name="parameters"></a>パラメーター

`code` <xref:System.Int32>

HTTP 状態コード (など) `404` 。

### <a name="return-value"></a>戻り値

<xref:System.String?displayProperty=nameWithType>

HTTP 状態の説明。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
