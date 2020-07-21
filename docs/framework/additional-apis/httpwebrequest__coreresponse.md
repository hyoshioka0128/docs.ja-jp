---
title: _CoreResponse HttpWebRequest フィールド
description: .NET の _CoreResponse HttpWebRequest フィールドについて確認します。 このフィールドは、HTTP 応答解析の結果を含む CoreResponseData または Exception オブジェクトです。
ms.date: 01/29/2018
topic_type:
- apiref
api_name:
- System.Net.HttpWebRequest._CoreResponse
api_location:
- System.dll
api_type:
- Assembly
author: stevewhims
ms.openlocfilehash: 5093ec7ed2c3b94931dcd622ae9ccdb42feffa18
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989751"
---
# <a name="httpwebrequest_coreresponse-field"></a>HttpWebRequest。 \_CoreResponse フィールド

`HttpWebRequest._CoreResponse`は、 [CoreResponseData](coreresponsedata.md) <xref:System.Exception> HTTP 応答の解析結果を含むオブジェクト (CoreResponseData または) です。

## <a name="syntax"></a>構文
  
```csharp
private object _CoreResponse
```

> [!WARNING]
> この API は、コード内で直接使用するためのものではありません。 代わりに、を使用して <xref:System.Diagnostics.DiagnosticSource> ネットワークコードをフックする必要があります。 「 [DiagnosticSource User'S Guide](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md)」を参照してください。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)

**.NET Framework のバージョン:** 2.0 以降で使用できます。
