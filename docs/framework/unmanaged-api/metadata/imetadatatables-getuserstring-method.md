---
title: IMetaDataTables::GetUserString メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetUserString
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetUserString
helpviewer_keywords:
- IMetaDataTables::GetUserString method [.NET Framework metadata]
- GetUserString method, IMetaDataTables interface [.NET Framework metadata]
ms.assetid: 35b8f0d6-9aba-4714-adb2-62020a38fb7e
topic_type:
- apiref
ms.openlocfilehash: 21ce66722e069573b651ada950b64ef6d97220fb
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501145"
---
# <a name="imetadatatablesgetuserstring-method"></a>IMetaDataTables::GetUserString メソッド

現在のスコープ内の文字列列にある、指定したインデックス位置にあるハードコーディングされた文字列を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetUserString (
    [in]  ULONG       ixUserString,
    [out] ULONG       *pcbData,
    [out] const void  **ppData
);
```

## <a name="parameters"></a>パラメーター

`ixUserString`\
からハードコーディングされた文字列の取得元のインデックス値。

`pcbData`\
入出力のサイズへのポインター `ppData` 。

`ppData`\
入出力返された文字列へのポインターへのポインター。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** Cor

**ライブラリ:** Mscoree.dll のリソースとして使用されます。

**.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>関連項目

- [IMetaDataTables インターフェイス](imetadatatables-interface.md)
- [IMetaDataTables2 インターフェイス](imetadatatables2-interface.md)
