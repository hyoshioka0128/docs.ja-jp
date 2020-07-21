---
title: IHostMemoryManager::VirtualProtect メソッド
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualProtect
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualProtect
helpviewer_keywords:
- IHostMemoryManager::VirtualProtect method [.NET Framework hosting]
- VirtualProtect method [.NET Framework hosting]
ms.assetid: 13be0299-df0d-4951-aabf-0676a30b385f
topic_type:
- apiref
ms.openlocfilehash: 473a52b55f793abc76883b0a5cd5b2a04756d9f7
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804353"
---
# <a name="ihostmemorymanagervirtualprotect-method"></a>IHostMemoryManager::VirtualProtect メソッド
対応する Win32 関数の論理ラッパーとして機能します。 の Win32 実装では、 `VirtualProtect` 呼び出し元プロセスの仮想アドレス空間でコミットされたページの領域の保護が変更されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT VirtualProtect (  
    [in]  void*   lpAddress,  
    [in]  SIZE_T  dwSize,  
    [in]  DWORD   flNewProtect,  
    [out] DWORD*  pflOldProtect  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `lpAddress`  
 から保護属性が変更される仮想メモリのベースアドレスへのポインター。  
  
 `dwSize`  
 から変更するメモリページの領域のサイズ (バイト単位)。  
  
 `flNewProtect`  
 から適用するメモリ保護の種類。  
  
 `pflOldProtect`  
 入出力以前のメモリ保護値へのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`VirtualProtect`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 のこの実装 `VirtualProtect` は HRESULT 値を返しますが、Win32 実装は成功を示す0以外の値を返し、エラーを示す0の値を返します。 詳細については、Windows プラットフォームのドキュメントを参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)
