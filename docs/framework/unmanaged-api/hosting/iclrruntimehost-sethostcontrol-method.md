---
title: ICLRRuntimeHost::SetHostControl メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.SetHostControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::SetHostControl
helpviewer_keywords:
- SetHostControl method [.NET Framework hosting]
- ICLRRuntimeHost::SetHostControl method [.NET Framework hosting]
ms.assetid: 6136be87-e631-4756-81ed-74b66581bad4
topic_type:
- apiref
ms.openlocfilehash: 644b31ae8e8f0c51c08bcad57220a028406cfd3a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504076"
---
# <a name="iclrruntimehostsethostcontrol-method"></a>ICLRRuntimeHost::SetHostControl メソッド
[IHostControl インターフェイス](ihostcontrol-interface.md)のホストの実装を取得するために共通言語ランタイム (CLR) が使用できるインターフェイスポインターを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetHostControl(  
    [in] IHostControl* pHostControl  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pHostControl`  
 から[IHostControl インターフェイス](ihostcontrol-interface.md)のホストの実装へのインターフェイスポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetHostControl`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返す場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_CLR_ALREADY_STARTED|CLR は既に初期化されています。|  
  
## <a name="remarks"></a>解説  
 CLR が初期化される前にを呼び出す必要があり `SetHostControl` ます。つまり、 [Start メソッド](iclrruntimehost-start-method.md)を呼び出すか、任意の[メタデータインターフェイス](../metadata/metadata-interfaces.md)を使用します。 `SetHostControl` [Corbindtoの entruntime 関数](corbindtocurrentruntime-function.md)または[Corbindtocurrentruntime 関数](corbindtoruntimeex-function.md)を呼び出した直後にを呼び出すことをお勧めします。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)
- [IHostControl インターフェイス](ihostcontrol-interface.md)
