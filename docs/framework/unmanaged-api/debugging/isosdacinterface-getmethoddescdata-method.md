---
title: 'ISOSDacInterface:: GetMethodDescData メソッド'
ms.date: 01/16/2019
api.name:
- ISOSDacInterface::GetMethodDescData Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- ISOSDacInterface::GetMethodDescData Method
helpviewer.keywords:
- ISOSDacInterface::GetMethodDescData Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 105149d0abf312c33a8498e7428e3a8b23d6ae7d
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421021"
---
# <a name="isosdacinterfacegetmethoddescdata-method"></a>ISOSDacInterface:: GetMethodDescData メソッド

指定された MethodDesc ポインターのデータを取得します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT GetMethodDescData(
    CLRDATA_ADDRESS            methodDesc,
    CLRDATA_ADDRESS            ip,
    DacpMethodDescData *data,
    ULONG                      cRevertedRejitVersions,
    DacpReJitData      *rgRevertedRejitData,
    void                      *pcNeededRevertedRejitData
);
```

## <a name="parameters"></a>パラメーター

`methodDesc`\
からMethodDesc のアドレス。

`ip`\
からメソッドの IP アドレス。

`data`\
入出力内部 Api から返される MethodDesc に関連付けられたデータ。

`cRevertedRejitVersions`\
入出力戻された再 jit バージョンの数。

`rgRevertedRejitData`\
入出力内部 Api から返された、元に戻された rejit バージョンに関連付けられたデータ。

`pcNeededRevertedRejitData`\
入出力戻された ReJit バージョンに関連付けられたデータを格納するために必要なバイト数。

## <a name="remarks"></a>解説

指定されたメソッドはインターフェイスの一部で `ISOSDacInterface` あり、仮想メソッドテーブルの21スロットに対応します。 これらを使用できるようにするには、を [`CLRDATA_ADDRESS`](../common-data-types-unmanaged-api-reference.md) 64 ビット符号なし整数として定義する必要があります。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [ISOSDacInterface インターフェイス](isosdacinterface-interface.md)
