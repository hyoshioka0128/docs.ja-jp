---
title: 'IXCLRDataMethodDefinition:: EndEnumInstances メソッド'
ms.date: 01/16/2019
api.name:
- IXCLRDataMethodDefinition::EndEnumInstances Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodDefinition::EndEnumInstances Method
helpviewer.keywords:
- IXCLRDataMethodDefinition::EndEnumInstances Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 7271c9594a679af205c404f59ff6731821aa0acf
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420995"
---
# <a name="ixclrdatamethoddefinitionendenuminstances-method"></a>IXCLRDataMethodDefinition:: EndEnumInstances メソッド

インスタンスの列挙中に使用される内部反復子によって使用されるリソースを解放します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT EndEnumInstances(
    [in] CLRDATA_ENUM handle
);
```

## <a name="parameters"></a>パラメーター

`handle`\
入出力インスタンスを列挙するハンドル。

## <a name="remarks"></a>解説

指定されたメソッドはインターフェイスの一部で `IXCLRDataMethodDefinition` あり、仮想メソッドテーブルの7番目のスロットに対応します。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [IXCLRDataMethodDefinition インターフェイス](ixclrdatamethoddefinition-interface.md)
