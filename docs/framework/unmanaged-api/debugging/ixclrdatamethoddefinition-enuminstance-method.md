---
title: 'IXCLRDataMethodDefinition:: EnumInstance メソッド'
ms.date: 01/16/2019
api.name:
- IXCLRDataMethodDefinition::EnumInstance Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataMethodDefinition::EnumInstance Method
helpviewer.keywords:
- IXCLRDataMethodDefinition::EnumInstance Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: ae1ef2a3c8cf9e042ab9ab233ed993f8e36b2fce
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420943"
---
# <a name="ixclrdatamethoddefinitionenuminstance-method"></a>IXCLRDataMethodDefinition:: EnumInstance メソッド

このメソッド定義のインスタンスを列挙します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT EnumInstance(
    [in, out] CLRDATA_ENUM         *handle,
    [out] IXCLRDataMethodInstance **instance
);
```

## <a name="parameters"></a>パラメーター

`handle`\
[入力、出力]インスタンスを列挙するハンドル。

`instance`\
入出力列挙されたインスタンス。

## <a name="remarks"></a>解説

指定されたメソッドはインターフェイスの一部で `IXCLRDataMethodDefinition` あり、仮想メソッドテーブルの6番目のスロットに対応します。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [CLRDataSourceType 列挙型](clrdatasourcetype-enumeration.md)
- [デバッグ](index.md)
- [IXCLRDataMethodDefinition インターフェイス](ixclrdatamethoddefinition-interface.md)
- [IXCLRDataMethodInstance インターフェイス](ixclrdatamethodinstance-interface.md)
