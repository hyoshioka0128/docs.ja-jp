---
title: 'ISOSDacInterface:: GetModuleData メソッド'
ms.date: 02/01/2019
api.name:
- ISOSDacInterface::GetModuleData Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- ISOSDacInterface::GetModuleData Method
helpviewer.keywords:
- ISOSDacInterface::GetModuleData Method [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: b302100eb6cbfa83896cd358762c496ea01f7509
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420982"
---
# <a name="isosdacinterfacegetmoduledata-method"></a>ISOSDacInterface:: GetModuleData メソッド

指定したアドレスに読み込まれたモジュールに対応するデータをフェッチします。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT GetModuleData(
    CLRDATA_ADDRESS moduleAddr,
    DacpModuleData *data
);
```

## <a name="parameters"></a>パラメーター

`moduleAddr`\
から情報を取得するモジュールのアドレス。

`data`\
入出力読み込まれたモジュールの情報を保持する[Dacpmoduledata 構造体](dacpmoduledata-structure.md)。

## <a name="remarks"></a>解説

指定されたメソッドはインターフェイスの一部で `ISOSDacInterface` あり、仮想メソッドテーブルの14番目のスロットに対応します。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [ISOSDacInterface インターフェイス](isosdacinterface-interface.md)
