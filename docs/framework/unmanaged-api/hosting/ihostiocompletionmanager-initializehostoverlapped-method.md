---
title: IHostIoCompletionManager::InitializeHostOverlapped メソッド
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.InitializeHostOverlapped
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped
helpviewer_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped method [.NET Framework hosting]
- InitializeHostOverlapped method [.NET Framework hosting]
ms.assetid: c35199bf-bc47-4901-b467-4e8a37644bbb
topic_type:
- apiref
ms.openlocfilehash: cf257ab86d27946c861c89dff5e6f09a42013e58
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804706"
---
# <a name="ihostiocompletionmanagerinitializehostoverlapped-method"></a>IHostIoCompletionManager::InitializeHostOverlapped メソッド
非同期 i/o 要求に使用される Win32 構造体に追加するカスタムデータを初期化する機会をホストに提供し `OVERLAPPED` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT InitializeHostOverlapped (  
    [in] void* pvOverlapped  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pvOverlapped`  
 から`OVERLAPPED`I/o 要求に含まれる Win32 構造体へのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`InitializeHostOverlapped`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|要求されたリソースを割り当てるのに十分なメモリがありませんでした。|  
  
## <a name="remarks"></a>解説  
 Windows プラットフォーム関数は、構造体を使用して `OVERLAPPED` 非同期 i/o 要求の状態を格納します。 CLR は、メソッドを呼び出して、 `InitializeHostOverlapped` ホストにカスタムデータをインスタンスに追加する機会を与え `OVERLAPPED` ます。  
  
> [!IMPORTANT]
> カスタムデータブロックの先頭に到達するには、ホストで、オフセットを構造体のサイズ () に設定する必要があり `OVERLAPPED` `sizeof(OVERLAPPED)` ます。  
  
 E_OUTOFMEMORY の戻り値は、ホストがカスタムデータを初期化できなかったことを示します。 この場合、CLR はエラーを報告し、呼び出しに失敗します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRIoCompletionManager インターフェイス](iclriocompletionmanager-interface.md)
- [GetHostOverlappedSize メソッド](ihostiocompletionmanager-gethostoverlappedsize-method.md)
- [IHostIoCompletionManager インターフェイス](ihostiocompletionmanager-interface.md)
