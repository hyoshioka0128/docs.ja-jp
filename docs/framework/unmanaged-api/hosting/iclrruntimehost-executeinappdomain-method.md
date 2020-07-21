---
title: ICLRRuntimeHost::ExecuteInAppDomain メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.ExecuteInAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::ExecuteInAppDomain
helpviewer_keywords:
- ICLRRuntimeHost::ExecuteInAppDomain method [.NET Framework hosting]
- ExecuteInAppDomain method [.NET Framework hosting]
ms.assetid: e2b0e2db-3fae-4b56-844e-d30a125a660c
topic_type:
- apiref
ms.openlocfilehash: 505c16cb7ead7950b6d2d6d401730cc3368fb6aa
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703301"
---
# <a name="iclrruntimehostexecuteinappdomain-method"></a>ICLRRuntimeHost::ExecuteInAppDomain メソッド
指定し <xref:System.AppDomain> たマネージコードを実行するを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ExecuteInAppDomain(  
    [in] DWORD AppDomainId,
    [in] FExecuteInDomainCallback pCallback,
    [in] void* cookie  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `AppDomainId`  
 から<xref:System.AppDomain>指定したメソッドを実行するの数値 ID。  
  
 `pCallback`  
 から指定した内で実行する関数へのポインター <xref:System.AppDomain> 。  
  
 `cookie`  
 から非透過的な呼び出し元に割り当てられたメモリへのポインター。 このパラメーターは、共通言語ランタイム (CLR) によってドメインコールバックに渡されます。 ランタイムによって管理されるヒープメモリではありません。このメモリの割り当てと有効期間は、どちらも呼び出し元によって制御されます。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`ExecuteInAppDomain`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返す場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 `ExecuteInAppDomain`指定したマネージメソッドを実行する管理対象をホストで制御できるように <xref:System.AppDomain> します。 アプリケーションドメインの識別子の値を取得できます。これは、 <xref:System.AppDomain.Id%2A> [GetCurrentAppDomainId メソッド](iclrruntimehost-getcurrentappdomainid-method.md)を呼び出すことによって、プロパティの値に対応します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)
