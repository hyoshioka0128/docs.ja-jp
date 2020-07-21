---
title: IHostMemoryManager::VirtualAlloc メソッド
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualAlloc
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualAlloc
helpviewer_keywords:
- VirtualAlloc method [.NET Framework hosting]
- IHostMemoryManager::VirtualAlloc method [.NET Framework hosting]
ms.assetid: 4dff3646-a050-4bd9-ac31-fe307e8637ec
topic_type:
- apiref
ms.openlocfilehash: de41b5e0aaf835ee2d4e4f32696fe104d5830b57
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804447"
---
# <a name="ihostmemorymanagervirtualalloc-method"></a>IHostMemoryManager::VirtualAlloc メソッド
対応する Win32 関数の論理ラッパーとして機能します。 の Win32 実装は、 `VirtualAlloc` 呼び出し元プロセスの仮想アドレス空間にあるページの領域を予約またはコミットします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT VirtualAlloc (  
    [in]  void*   pAddress,  
    [in]  SIZE_T  dwSize,  
    [in]  DWORD   flAllocationType,  
    [in]  DWORD   flProtect,  
    [in]  EMemoryCriticalLevel dwCriticalLevel,  
    [out] void**  ppMem  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAddress`  
 から割り当てる領域の開始アドレスへのポインター。  
  
 `dwSize`  
 から領域のサイズ (バイト単位)。  
  
 `flAllocationType`  
 からメモリ割り当ての種類。  
  
 `flProtect`  
 から割り当てられるページの領域のメモリ保護。  
  
 `dwCriticalLevel`  
 から割り当てエラーの影響を示す[EMemoryCriticalLevel](ememorycriticallevel-enumeration.md)値です。  
  
 `ppMem`  
 入出力割り当てられたメモリの開始アドレスへのポインター。要求を満たすことができなかった場合は null。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`VirtualAlloc`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|割り当て要求を完了するのに十分なメモリがありませんでした|  
  
## <a name="remarks"></a>解説  
 を呼び出して、プロセスのアドレス空間にリージョンを予約し `VirtualAlloc` ます。 パラメーターには、 `pAddress` 必要なメモリブロックの開始アドレスが格納されます。 通常、このパラメーターは null に設定されます。 オペレーティングシステムは、プロセスで使用可能な空きアドレス範囲の記録を保持します。 値が null の場合は、 `pAddress` 必要に応じてリージョンを予約するようにシステムに指示します。 または、メモリブロックの特定の開始アドレスを指定することもできます。 どちらの場合も、出力パラメーター `ppMem` は、割り当てられたメモリへのポインターとして返されます。 関数自体は HRESULT 値を返します。  
  
 Win32 関数にはパラメーターがないため、 `VirtualAlloc` `ppMem` 代わりに割り当てられたメモリへのポインターを返します。 詳細については、Windows プラットフォームのドキュメントを参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)
