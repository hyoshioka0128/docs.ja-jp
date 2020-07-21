---
title: ICLRDataEnumMemoryRegions::EnumMemoryRegions メソッド
ms.date: 03/30/2017
api_name:
- ICLRDataEnumMemoryRegions.EnumMemoryRegions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataEnumMemoryRegions::EnumMemoryRegions
helpviewer_keywords:
- ICLRDataEnumMemoryRegions::EnumMemoryRegions method [.NET Framework debugging]
- EnumMemoryRegions method [.NET Framework debugging]
ms.assetid: 22d2e339-f174-40b5-a478-0b744501566f
topic_type:
- apiref
ms.openlocfilehash: e6cdc924df126e56d2e7c8c9cb8762ee88712fcc
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860702"
---
# <a name="iclrdataenummemoryregionsenummemoryregions-method"></a>ICLRDataEnumMemoryRegions::EnumMemoryRegions メソッド
指定されたメモリ領域を列挙します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumMemoryRegions (  
    [in] ICLRDataEnumMemoryRegionsCallback  *callback,  
    [in] ULONG32                            miniDumpFlags,  
    [in] CLRDataEnumMemoryFlags             clrFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `callback`  
 から結果をデバッガーに通知するために、列挙される各メモリ領域に対してこのメソッドによって呼び出される[ICLRDataEnumMemoryRegionsCallback](iclrdataenummemoryregionscallback-interface.md)インスタンスへのポインター。  
  
 コールバックがエラーを示す場合でも、メモリ領域の列挙は続行されます。  
  
 `miniDumpFlags`  
 から使用しません。  
  
 `clrFlags`  
 から列挙するメモリ領域を指定する[Clrdataenummemoryflags](clrdataenummemoryflags-enumeration.md)列挙体の値。  
  
## <a name="remarks"></a>解説  
 このメソッドは、指定された[ICLRDataEnumMemoryRegionsCallback](iclrdataenummemoryregionscallback-interface.md)インスタンスを使用して、結果を呼び出し元に通知します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ClrData .idl, ClrData .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRDataEnumMemoryRegions インターフェイス](iclrdataenummemoryregions-interface.md)
