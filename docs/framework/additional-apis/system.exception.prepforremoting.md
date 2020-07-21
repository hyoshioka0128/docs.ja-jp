---
title: PrepForRemoting メソッド (System)
description: .NET で PrepForRemoting メソッドを確認します。 メソッドは、クライアントで例外が再スローされる前に、サーバー側のスタックトレースをメッセージに追加します。
ms.date: 10/08/2019
topic_type:
- apiref
api_name:
- System.Exception.PrepForRemoting
api_location:
- mscorlib.dll
api_type:
- Assembly
ms.openlocfilehash: 9ceb73499ae3bb308975e6db5b961bfe40165ba3
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85105257"
---
# <a name="exceptionprepforremoting-method"></a>Exception.PrepForRemoting メソッド

クライアント呼び出しサイトで例外が再スローされる前に、サーバー側スタックトレースをメッセージに追加して保存します。

```csharp
internal Exception PrepForRemoting();
```

## <a name="returns"></a>戻り値

<xref:System.Exception>  
この <xref:System.Exception> インスタンス。

## <a name="remarks"></a>Remarks

> [!WARNING]
> `Exception.PrepForRemoting`メソッドは内部であり、コードで直接使用するためのものではありません。
>
> Microsoft では、どのような状況でも、実稼働アプリケーションでこの方法を使用することはサポートしていません。

## <a name="requirements"></a>必要条件

**名前空間:** <xref:System>

**アセンブリ:** mscorlib.dll (mscorlib.dll)

**.NET Framework のバージョン:** 1.0 以降で使用できます。
