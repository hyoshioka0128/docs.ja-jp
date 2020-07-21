---
title: 'IXCLRDataProcess:: StartEnumModules メソッド'
ms.date: 01/16/2019
api.name:
- IXCLRDataProcess::StartEnumModules Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataProcess::StartEnumModules Method
helpviewer.keywords:
- IXCLRDataProcess::StartEnumModules Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: d55b07ea3fada73237919bf677163a9096d5ad04
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420722"
---
# <a name="ixclrdataprocessstartenummodules-method"></a>IXCLRDataProcess:: StartEnumModules メソッド

プロセスのモジュールを列挙するハンドルを提供します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT StartEnumModules(
    [out] CLRDATA_ENUM *handle
);
```

## <a name="parameters"></a>パラメーター

`handle`\
入出力モジュールを列挙するハンドル。

## <a name="remarks"></a>解説

指定されたメソッドはインターフェイスの一部で `IXCLRDataProcess` あり、仮想メソッドテーブルの24番のスロットに対応します。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [CLRDataSourceType 列挙型](clrdatasourcetype-enumeration.md)
- [デバッグ](index.md)
- [IXCLRDataProcess インターフェイス](ixclrdataprocess-interface.md)
