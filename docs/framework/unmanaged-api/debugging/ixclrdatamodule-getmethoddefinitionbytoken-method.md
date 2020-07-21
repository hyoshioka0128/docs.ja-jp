---
title: 'IXCLRDataModule:: GetMethodDefinitionByToken メソッド'
ms.date: 01/16/2019
api.name:
- IXCLRDataModule::GetMethodDefinitionByToken Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataModule::GetMethodDefinitionByToken Method
helpviewer.keywords:
- IXCLRDataModule::GetMethodDefinitionByToken Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 074949145be588fc34266a9f2ee501caeeffb9d3
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420878"
---
# <a name="ixclrdatamodulegetmethoddefinitionbytoken-method"></a>IXCLRDataModule:: GetMethodDefinitionByToken メソッド

指定されたメタデータトークンに対応するメソッド定義を取得します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT GetMethodDefinitionByToken(
    [in] mdMethodDef token,
    [out] IXCLRDataMethodDefinition** methodDefinition
);
```

## <a name="parameters"></a>パラメーター

`token`\
からメソッドトークン。

`methodDefinition`\
入出力メソッドの定義。

## <a name="remarks"></a>解説

指定されたメソッドはインターフェイスの一部で `IXCLRDataModule` あり、仮想メソッドテーブルの26日スロットに対応します。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [IXCLRDataModule インターフェイス](ixclrdatamodule-interface.md)
