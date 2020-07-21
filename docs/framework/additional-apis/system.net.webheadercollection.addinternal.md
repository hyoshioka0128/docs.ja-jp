---
title: WebHeaderCollection. AddInternal メソッド (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.WebHeaderCollection.AddInternal
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: fd7b13ccd1baad48ab99a85d80ccd6154651c608
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990532"
---
# <a name="webheadercollectionaddinternal-method"></a>WebHeaderCollection. AddInternal メソッド

指定された名前と値を持つ新しいヘッダーをコレクションに追加し、チェックをバイパスします。

```csharp
internal void AddInternal(string name, string value)
```

> [!WARNING]
> このメソッドは内部であり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでこの方法を使用することはサポートしていません。

## <a name="parameters"></a>パラメーター

- `name` <xref:System.String>

  ヘッダーの名前。

- `value` <xref:System.String>

  ヘッダーの値です。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
