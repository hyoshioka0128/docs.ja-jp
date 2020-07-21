---
title: IHostMemoryManager::VirtualFree メソッド
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualFree
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualFree
helpviewer_keywords:
- IHostMemoryManager::VirtualFree method [.NET Framework hosting]
- VirtualFree method [.NET Framework hosting]
ms.assetid: 1a436e89-eb28-4d15-bcf1-a072f86dbd99
topic_type:
- apiref
ms.openlocfilehash: 4d37b7d803509ebfa861b7502d419f868bd12e11
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804384"
---
# <a name="ihostmemorymanagervirtualfree-method"></a>IHostMemoryManager::VirtualFree メソッド
対応する Win32 関数の論理ラッパーとして機能します。 `VirtualFree`リリース、デ、またはリリースの Win32 実装では、呼び出しプロセスの仮想アドレス空間内のページの領域をデします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT VirtualFree (  
    [in] LPVOID  lpAddress,  
    [in] SIZE_T  dwSize,  
    [in] DWORD   dwFreeType  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `lpAddress`  
 から解放される仮想メモリページのベースアドレスへのポインター。  
  
 `dwSize`  
 から解放する領域のサイズ (バイト単位)。  
  
 `dwFreeType`  
 から解放操作の種類。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`VirtualFree`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|HOST_E_INVALIDOPERATION|ホストを通じて割り当てられていないメモリを解放しようとしました。|  
  
## <a name="remarks"></a>解説  
 `VirtualFree``lpAddress` [IHostMemoryManager:: VirtualAlloc](ihostmemorymanager-virtualalloc-method.md)関数の以前の呼び出しによって、パラメーターに関連付けられた仮想メモリページを解放します。 ホストを通じて割り当てられていないメモリを解放しようとすると HOST_E_INVALIDOPERATION が返されます。  
  
 セマンティクスは、の Win32 実装のセマンティクスと同じです `VirtualFree` 。 詳細については、Windows プラットフォームのドキュメントを参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)
- [IHostMalloc インターフェイス](ihostmalloc-interface.md)
