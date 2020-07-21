---
title: IMetaDataTables::GetColumnInfo メソッド
ms.date: 10/10/2019
api_name:
- IMetaDataTables.GetColumnInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetColumnInfo
helpviewer_keywords:
- IMetaDataTables::GetColumnInfo method [.NET Framework metadata]
- GetColumnInfo method [.NET Framework metadata]
ms.assetid: 68c160ea-ae7d-4750-985d-a038b2c8e7d9
topic_type:
- apiref
ms.openlocfilehash: a044924810016eea60682b8765aeee448b552f0d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501197"
---
# <a name="imetadatatablesgetcolumninfo-method"></a>IMetaDataTables::GetColumnInfo メソッド
指定されたテーブル内の指定された列に関するデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetColumnInfo (
    [in]  ULONG        ixTbl,  
    [in]  ULONG        ixCol,  
    [out] ULONG        *poCol,  
    [out] ULONG        *pcbCol,  
    [out] ULONG        *pType,  
    [out] const char   **ppName  
);  
```  
  
## <a name="parameters"></a>パラメーター
=======

 `ixTbl`  
 から目的のテーブルのインデックス。  
  
 `ixCol`  
 から目的の列のインデックス。  
  
 `poCol`  
 入出力行内の列のオフセットへのポインター。  
  
 `pcbCol`  
 入出力列のサイズ (バイト単位) へのポインター。  
  
 `pType`  
 入出力列内の値の型へのポインター。  
  
 `ppName`  
 入出力列名へのポインターへのポインター。  

## <a name="remarks"></a>解説

返される列の型は、値の範囲内にあります。

| pType                    | 説明   | ヘルパー関数                   |
|--------------------------|---------------|-----------------------------------|
| `0`..`iRidMax`<br>(0.. 63)   | Rid           | **IsRidType**<br>**IsRidOrToken** |
| `iCodedToken`..`iCodedTokenMax`<br>(64.. 95) | コード化されたトークン | **IsCodedTokenType** <br>**IsRidOrToken** |
| `iSHORT`(96)            | Int16         | **IsFixedType**                   |
| `iUSHORT`(97)           | UInt16        | **IsFixedType**                   |
| `iLONG`(98)             | Int32         | **IsFixedType**                   |
| `iULONG`(99)            | UInt32        | **IsFixedType**                   |
| `iBYTE`(100)            | Byte          | **IsFixedType**                   |
| `iSTRING`(101)          | String        | **IsHeapType**                    |
| `iGUID`(102)            | Guid          | **IsHeapType**                    |
| `iBLOB`(103)            | BLOB          | **IsHeapType**                    |

*ヒープ*に格納されている値 (つまり、 `IsHeapType == true` ) は次を使用して読み取ることができます。

- `iSTRING`: **Imetadatatables**
- `iGUID`: **Imetadatatables 実行できます。 GetGUID**
- `iBLOB`: **Imetadatatables 実行できます。 GetBlob**

> [!IMPORTANT]
> 上の表で定義されている定数を使用するには、 `#define _DEFINE_META_DATA_META_CONSTANTS` *cor*ヘッダーファイルによって提供されるディレクティブをインクルードします。

## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataTables インターフェイス](imetadatatables-interface.md)
- [IMetaDataTables2 インターフェイス](imetadatatables2-interface.md)
