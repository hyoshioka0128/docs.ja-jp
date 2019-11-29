---
title: Message. BodyToString メソッド (System.servicemodel)
author: mairaw
ms.author: mairaw
ms.date: 11/01/2019
topic_type:
- apiref
api_name:
- System.ServiceModel.Channels.Message.BodyToString
api_location:
- system.servicemodel.dll
api_type:
- Assembly
ms.openlocfilehash: 7b0b56bfda1c0c37f43f95e9684d3b4042c1b97c
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74451312"
---
# <a name="messagebodytostring-method"></a>Message. BodyToString メソッド

<xref:System.ServiceModel.Channels.Message.OnBodyToString%2A?displayProperty=nameWithType> メソッドを呼び出すことによって、メッセージ本文を文字列に変換します。

```csharp
internal void BodyToString(XmlDictionaryWriter writer);
```

## <a name="parameters"></a>パラメーター

- `writer` <xref:System.Xml.XmlDictionaryWriter>\
  メッセージ本文を文字列に変換するために使用されるライター。

## <a name="remarks"></a>コメント

> [!WARNING]
> `Message.BodyToString` メソッドは内部であり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでこの方法を使用することはサポートしていません。

## <a name="requirements"></a>要件

**名前空間:** <xref:System.ServiceModel.Channels>

**アセンブリ:** System.servicemodel

**.NET Framework のバージョン:** 3.0 以降で使用できます。
