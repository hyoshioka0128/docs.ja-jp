---
title: DacpGetModuleAddress::Request メソッド
ms.date: 01/16/2019
api.name:
- DacpGetModuleAddress::Request Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpGetModuleAddress::Request Method
helpviewer.keywords:
- DacpGetModuleAddress::Request Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 1755526636bed6d78663112e4c2ad5ab7c3f731c
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860844"
---
# <a name="dacpgetmoduleaddressrequest-method"></a>DacpGetModuleAddress::Request メソッド

指定されたランタイム構造体を構造体に設定する要求を実行します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT Request(
    [in] IXCLRDataModule* pDataModule
);
```

## <a name="parameters"></a>パラメーター

`pDataModule`\
からシードデータモジュールへのポインター。

## <a name="remarks"></a>解説

この構造体はランタイム内に存在し、ヘッダーまたはライブラリファイルを介して公開されることはありません。 これを使用する最も簡単な方法は、実装を模倣することです。

- 次のパラメーターを使用して`Request` 、 `IXCLRDataModule*`パラメーターのメソッドの呼び出しから取得した値を返します。`((uint32) 0xf0000000, 0, 0, (uint32) sizeof(*this), (uint8*) this)`

## <a name="requirements"></a>必要条件

**プラットフォーム:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。\
**ヘッダー:** 存在
**ライブラリ:** 存在
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [DacpGetModuleAddress 構造体](dacpgetmoduleaddress-structure.md)
