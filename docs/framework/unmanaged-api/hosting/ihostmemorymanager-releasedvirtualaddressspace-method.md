---
title: IHostMemoryManager::ReleasedVirtualAddressSpace メソッド
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.ReleasedVirtualAddressSpace
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::ReleasedVirtualAddressSpace
helpviewer_keywords:
- ReleasedVirtualAddressSpace method [.NET Framework hosting]
- IHostMemoryManager::ReleasedVirtualAddressSpace method [.NET Framework hosting]
ms.assetid: d1876601-6ab9-48e1-8ebd-184af1d0cd76
topic_type:
- apiref
ms.openlocfilehash: 4a246fb95ab5b4a7f187aa660f20e590c63ddff2
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804467"
---
# <a name="ihostmemorymanagerreleasedvirtualaddressspace-method"></a>IHostMemoryManager::ReleasedVirtualAddressSpace メソッド
指定されたメモリを使用して共通言語ランタイム (CLR) が終了したことをホストに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ReleasedVirtualAddressSpace(  
    [in] LPVOID startAddress  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `startAddress`  
 から解放されるメモリの開始アドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 `ReleasedVirtualAddressSpace`メソッドはコールバックメソッドであり、ホストアプリケーションのライターによって実装される必要があります。 これは CLR によって呼び出されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)
