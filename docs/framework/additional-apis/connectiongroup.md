---
title: ConnectionGroup クラス
description: ConnectionGroup クラスについて説明します。このクラスは、ServicePoint コンテキスト内で接続をグループ化し、.NET のネットワークリソースのコンテキストを維持するために使用されます。
ms.date: 05/01/2017
topic_type:
- apiref
api_name:
- System.Net.ConnectionGroup
api_location:
- System.dll
api_type:
- Assembly
ms.assetid: 25c08217-fdeb-44b9-9cd6-1b4955d6e602
ms.openlocfilehash: 7121713b26880f2490b40d59d92d431a567519b3
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84989817"
---
# <a name="connectiongroup-class"></a>ConnectionGroup クラス

クラスは、 `ConnectionGroup` コンテキスト内の接続の一覧をグループ化 <xref:System.Net.ServicePoint> し、ネットワークリソース (プロキシや個別のクライアントなど) のコンテキストを維持するために使用されます。

## <a name="syntax"></a>構文
  
```csharp  
internal class ConnectionGroup
```

> [!WARNING]
> `ConnectionGroup`クラスは内部であり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでのこのクラスの使用はサポートしていません。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System.Net>

**アセンブリ:** システム (System.dll)

**.NET Framework のバージョン:** 2.0 以降で使用できます。
