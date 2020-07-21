---
title: M_ResponseHeaders CoreResponseData フィールド
description: .NET の m_ResponseHeaders CoreResponseData フィールドについて説明します。 このフィールドは、サーバー応答に関連付けられたヘッダーを持つ WebHeaderCollection 型です。
ms.date: 01/29/2018
topic_type:
- apiref
api_name:
- System.Net.CoreResponseData.m_ResponseHeaders
api_location:
- System.dll
api_type:
- Assembly
author: stevewhims
ms.openlocfilehash: 7c7b896193cb81e9fc9e3ec28110359003a36728
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989784"
---
# <a name="coreresponsedatam_responseheaders-field"></a>CoreResponseData \_ ResponseHeaders フィールド

`CoreResponseData.m_ResponseHeaders`は、 <xref:System.Net.WebHeaderCollection> サーバーの応答に関連付けられているヘッダーのです。

## <a name="syntax"></a>構文
  
```csharp
public WebHeaderCollection m_ResponseHeaders
```

> [!WARNING]
> この API は、コード内で直接使用するためのものではありません。 代わりに、を使用して <xref:System.Diagnostics.DiagnosticSource> ネットワークコードをフックする必要があります。 「 [DiagnosticSource User'S Guide](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md)」を参照してください。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)

**.NET Framework のバージョン:** 2.0 以降で使用できます。
