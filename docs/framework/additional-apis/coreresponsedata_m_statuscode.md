---
title: M_StatusCode CoreResponseData フィールド
description: .NET の m_StatusCode CoreResponseData フィールドについて確認します。 フィールドは、HTTP 応答の状態を含む HttpStatusCode 型です。
ms.date: 01/29/2018
topic_type:
- apiref
api_name:
- System.Net.CoreResponseData.m_StatusCode
api_location:
- System.dll
api_type:
- Assembly
author: stevewhims
ms.openlocfilehash: 05950290bde96511432941ce679e663126878663
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989777"
---
# <a name="coreresponsedatam_statuscode-field"></a>CoreResponseData \_ StatusCode フィールド

`CoreResponseData.m_StatusCode`<xref:System.Net.HttpStatusCode>応答の状態を表すです。

## <a name="syntax"></a>構文
  
```csharp
public HttpStatusCode m_StatusCode
```

> [!WARNING]
> この API は、コード内で直接使用するためのものではありません。 代わりに、を使用して <xref:System.Diagnostics.DiagnosticSource> ネットワークコードをフックする必要があります。 「 [DiagnosticSource User'S Guide](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md)」を参照してください。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)

**.NET Framework のバージョン:** 2.0 以降で使用できます。
