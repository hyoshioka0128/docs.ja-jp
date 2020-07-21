---
title: ICLRControl::GetCLRManager メソッド
ms.date: 03/30/2017
api_name:
- ICLRControl.GetCLRManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRControl::GetCLRManager
helpviewer_keywords:
- GetCLRManager method [.NET Framework hosting]
- ICLRControl::GetCLRManager method [.NET Framework hosting]
ms.assetid: 8a11bfa4-cbb0-4082-82b5-f9fba66c93f5
topic_type:
- apiref
ms.openlocfilehash: 04cb45cd021532b6cb3d74a195cbd62e1ab8d31d
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615853"
---
# <a name="iclrcontrolgetclrmanager-method"></a>ICLRControl::GetCLRManager メソッド
ホストが共通言語ランタイム (CLR) を構成するために使用できる任意のマネージャー型のインスタンスへのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCLRManager (  
    [in]  REFIID  riid,  
    [out] void  **ppObject  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `riid`  
 から`IID`返されるマネージャーの型の。 次の `IID` 値がサポートされています。  
  
- IID_ICLRDebugManager: が ICLRDebugManager 型であることを指定し `ppObject` ます。 [ICLRDebugManager](iclrdebugmanager-interface.md)  
  
- IID_ICLRErrorReportingManager: が ICLRErrorReportingManager 型であることを指定し `ppObject` ます。 [ICLRErrorReportingManager](iclrerrorreportingmanager-interface.md)  
  
- IID_ICLRGCManager: が ICLRGCManager 型であることを指定し `ppObject` ます。 [ICLRGCManager](iclrgcmanager-interface.md)  
  
- IID_ICLRHostProtectionManager: が ICLRHostProtectionManager 型であることを指定し `ppObject` ます。 [ICLRHostProtectionManager](iclrhostprotectionmanager-interface.md)  
  
- IID_ICLROnEventManager: が ICLROnEventManager 型であることを指定し `ppObject` ます。 [ICLROnEventManager](iclroneventmanager-interface.md)  
  
- IID_ICLRPolicyManager: が ICLRPolicyManager 型であることを指定し `ppObject` ます。 [ICLRPolicyManager](iclrpolicymanager-interface.md)  
  
- IID_ICLRTaskManager: が ICLRTaskManager 型であることを指定し `ppObject` ます。 [ICLRTaskManager](iclrtaskmanager-interface.md)  
  
 `ppObject`  
 入出力要求されたマネージャーへのインターフェイスポインター。無効なマネージャーの種類が要求された場合は null。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドから正常に値が返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_NOINTERFACE|インターフェイス型はサポートされていません。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [IHostControl インターフェイス](ihostcontrol-interface.md)
