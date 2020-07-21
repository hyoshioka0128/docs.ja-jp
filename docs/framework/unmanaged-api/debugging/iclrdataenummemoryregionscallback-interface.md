---
title: ICLRDataEnumMemoryRegionsCallback インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRDataEnumMemoryRegionsCallback
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataEnumMemoryRegionsCallback
helpviewer_keywords:
- ICLRDataEnumMemoryRegionsCallback interface [.NET Framework debugging]
ms.assetid: 3f1af8b0-8478-48e0-a7ec-3e90e0b97649
topic_type:
- apiref
ms.openlocfilehash: ddcb8064dfb9be30c66404a8762a9ca73cd6afe4
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860661"
---
# <a name="iclrdataenummemoryregionscallback-interface"></a>ICLRDataEnumMemoryRegionsCallback インターフェイス
[ICLRDataEnumMemoryRegions:: EnumMemoryRegions](iclrdataenummemoryregions-enummemoryregions-method.md)のコールバックメソッドを提供し、指定されたメモリ領域を列挙しようとした結果をデバッガーに報告します。  
  
## <a name="methods"></a>メソッド  
  
|Method|説明|  
|------------|-----------------|  
|[EnumMemoryRegion メソッド](iclrdataenummemoryregionscallback-enummemoryregion-method.md)|指定さ`ICLRDataEnumMemoryRegions::EnumMemoryRegions`れたメモリ領域を列挙しようとした結果をデバッガーに報告するために、によって呼び出されます。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ClrData .idl, ClrData .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
