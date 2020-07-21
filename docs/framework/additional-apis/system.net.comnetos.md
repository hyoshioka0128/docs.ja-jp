---
title: ComNetOS クラス (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.ComNetOS
- System.Net.ComNetOS.IsWin7orLater
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: ed2b970d07df2c338870b386e75c1688703f1d68
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990546"
---
# <a name="comnetos-class"></a>ComNetOS クラス

バージョンやインストールの種類 (クライアントまたはサーバー) など、現在のオペレーティングシステムに関する情報を提供します。 このクラスは継承できません。
  
```csharp  
internal static class ComNetOS
```

> [!WARNING]
> このクラスは内部的なものであり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="iswin7orlater-field"></a>IsWin7orLater フィールド

オペレーティングシステムのバージョンが Windows 7 以降であるかどうかを指定します。

```csharp
internal static readonly bool IsWin7orLater
```

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)
