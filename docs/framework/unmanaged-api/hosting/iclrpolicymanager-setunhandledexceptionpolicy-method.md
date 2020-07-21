---
title: ICLRPolicyManager::SetUnhandledExceptionPolicy メソッド
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager.SetUnhandledExceptionPolicy
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager::SetUnhandledExceptionPolicy
helpviewer_keywords:
- ICLRPolicyManager::SetUnhandledExceptionPolicy method [.NET Framework hosting]
- SetUnhandledExceptionPolicy method [.NET Framework hosting]
ms.assetid: 5268480e-280a-4931-b7a3-dc3ffdf7f78f
topic_type:
- apiref
ms.openlocfilehash: 7fa02c4c79da118543117aada7d1b9cca09c4cae
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703407"
---
# <a name="iclrpolicymanagersetunhandledexceptionpolicy-method"></a>ICLRPolicyManager::SetUnhandledExceptionPolicy メソッド
未処理の例外が発生した場合の共通言語ランタイム (CLR) の動作を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetUnhandledExceptionPolicy (  
    [in] EClrUnhandledExceptionPolicy policy  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `policy`  
 から[EClrUnhandledException](eclrunhandledexception-enumeration.md)値の1つ。動作が CLR またはホストによって設定されているかどうかを示します。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetUnhandledExceptionPolicy`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 既定では、CLR はすべてのハンドルされない例外の最終的なハンドラーであり、既定の動作では、プロセスが破棄されます。 ホストはこの動作を変更できます。そのためには、 `policy` 値を Ehost決定 Edpolicy に設定します。 この値により、ホストは、以前のバージョンの CLR の場合と同様に、独自の既定の動作を実装できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrUnhandledException 列挙型](eclrunhandledexception-enumeration.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
- [IHostPolicyManager インターフェイス](ihostpolicymanager-interface.md)
