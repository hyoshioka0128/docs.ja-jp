---
title: ICLRMemoryNotificationCallback::OnMemoryNotification メソッド
ms.date: 03/30/2017
api_name:
- ICLRMemoryNotificationCallback.OnMemoryNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMemoryNotificationCallback::OnMemoryNotification
helpviewer_keywords:
- ICLRMemoryNotificationCallback::OnMemoryNotification method [.NET Framework hosting]
- OnMemoryNotification method [.NET Framework hosting]
ms.assetid: 5612a44d-56cc-4f34-af31-8c9809ba9431
topic_type:
- apiref
ms.openlocfilehash: d88abcc523eca06c8ec50cac2d2984b26099174a
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703790"
---
# <a name="iclrmemorynotificationcallbackonmemorynotification-method"></a>ICLRMemoryNotificationCallback::OnMemoryNotification メソッド
コンピューターのメモリ負荷の共通言語ランタイム (CLR) に通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OnMemoryNotification (  
    [in] EMemoryAvailable eMemoryAvailable  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `eMemoryAvailable`  
 から[EMemoryAvailable](ememoryavailable-enumeration.md)値の1つ。コンピューターが現在発生しているメモリ不足を示します。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`OnMemoryNotification`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 CLR は、 `OnMemoryNotification` [IHostMemoryManager:: RegisterMemoryNotificationCallback](ihostmemorymanager-registermemorynotificationcallback-method.md)メソッドの呼び出しを使用して、コールバックをに登録します。 ランタイムは、コールバックで返された情報を使用して、メモリリソースが不足していることをホストが報告したときに追加のメモリを解放します。  
  
> [!NOTE]
> を呼び出しても `OnMemoryNotification` ブロックされません。 常に直ちに返されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostMemoryManager インターフェイス](ihostmemorymanager-interface.md)
- [RegisterMemoryNotificationCallback メソッド](ihostmemorymanager-registermemorynotificationcallback-method.md)
- [ICLRMemoryNotificationCallback インターフェイス](iclrmemorynotificationcallback-interface.md)
