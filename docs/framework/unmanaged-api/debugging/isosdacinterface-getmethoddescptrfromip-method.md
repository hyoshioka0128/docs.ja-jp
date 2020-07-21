---
title: 'ISOSDacInterface:: GetMethodDescPtrFromIP メソッド'
ms.date: 02/01/2019
api.name:
- ISOSDacInterface::GetMethodDescPtrFromIP Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- ISOSDacInterface::GetMethodDescPtrFromIP Method
helpviewer.keywords:
- ISOSDacInterface::GetMethodDescPtrFromIP Method [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: c3de9e5ffe23a13c126343c6f74f042bf1239609
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421008"
---
# <a name="isosdacinterfacegetmethoddescptrfromip-method"></a>ISOSDacInterface:: GetMethodDescPtrFromIP メソッド

指定されたネイティブ命令アドレスを格納しているメソッドに対応する MethodDesc のポインターを取得します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT GetMethodDescPtrFromIP(
    CLRDATA_ADDRESS ip,
    CLRDATA_ADDRESS * ppMD
);
```

## <a name="parameters"></a>パラメーター

`ip`\
から実行時のメソッド内のアドレス。

`ppMD`\
入出力`MethodDesc`特定のメソッドののアドレス。

## <a name="remarks"></a>解説

指定されたメソッドは[ `ISOSDacInterface` インターフェイス](isosdacinterface-interface.md)の一部であり、仮想メソッドテーブルの22スロットに対応します。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [ISOSDacInterface インターフェイス](isosdacinterface-interface.md)
