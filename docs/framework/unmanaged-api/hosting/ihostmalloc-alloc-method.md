---
title: IHostMAlloc::Alloc メソッド
ms.date: 03/30/2017
api_name:
- IHostMAlloc.Alloc
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMAlloc::Alloc
helpviewer_keywords:
- Alloc method, IHostMAlloc interface [.NET Framework hosting]
- IHostMAlloc::Alloc method [.NET Framework hosting]
ms.assetid: a3007f5e-d75d-4b37-842b-704e9edced5e
topic_type:
- apiref
ms.openlocfilehash: 6f58e2290afa166d48306c0bbb50edd1df36888b
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804645"
---
# <a name="ihostmallocalloc-method"></a>IHostMAlloc::Alloc メソッド
ホストが指定された量のメモリをヒープから割り当てることを要求します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Alloc (  
    [in] SIZE_T  cbSize,
    [in] EMemoryCriticalLevel dwCriticalLevel,
    [out] void** ppMem  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cbSize`  
 から現在のメモリ割り当て要求のサイズ (バイト単位)。  
  
 `dwCriticalLevel`  
 から割り当てエラーの影響を示す[EMemoryCriticalLevel](ememorycriticallevel-enumeration.md)値の1つ。  
  
 `ppMem`  
 入出力割り当てられたメモリへのポインター。要求を完了できなかった場合は null。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`Alloc`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|割り当て要求を完了するのに十分なメモリがありませんでした。|  
  
## <a name="remarks"></a>解説  
 CLR は、 `IHostMalloc` [IHostMemoryManager:: CreateMalloc](ihostmemorymanager-createmalloc-method.md)メソッドを呼び出すことによって、インスタンスへのインターフェイスポインターを取得します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)
- [IHostMalloc インターフェイス](ihostmalloc-interface.md)
