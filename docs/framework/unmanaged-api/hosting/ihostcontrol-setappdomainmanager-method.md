---
title: IHostControl::SetAppDomainManager メソッド
ms.date: 03/30/2017
api_name:
- IHostControl.SetAppDomainManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostControl::SetAppDomainManager
helpviewer_keywords:
- IHostControl::SetAppDomainManager method [.NET Framework hosting]
- SetAppDomainManager method [.NET Framework hosting]
ms.assetid: 6562bbe7-0d67-4c50-a958-3a18cf680375
topic_type:
- apiref
ms.openlocfilehash: 74ffc5c92402808ae566d7cb014d9d920c384ae8
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804946"
---
# <a name="ihostcontrolsetappdomainmanager-method"></a>IHostControl::SetAppDomainManager メソッド
アプリケーションドメインが作成されたことをホストに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetAppDomainManager (  
    [in] DWORD     dwAppDomainID,  
    [in] IUnknown* pUnkAppDomainManager  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwAppDomainID`  
 から選択されたの数値識別子 <xref:System.AppDomain> 。  
  
 `pUnkAppDomainManager`  
 から<xref:System.AppDomainManager>ホストがとして実装しているオブジェクトへのポインター `IUnknown` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetAppDomainManager`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 は、 <xref:System.AppDomainManager> マネージコードにブートストラップし、それぞれの作成と設定を制御するためのメカニズムをホストに提供し <xref:System.AppDomain> ます。 は、作成される <xref:System.AppDomainManager> ときにそれぞれに読み込まれ <xref:System.AppDomain> <xref:System.AppDomain> ます。 このオプションを選択した場合、CLR は、パラメーターの値を設定することによって、アプリケーションドメインが作成されたことをホストに通知 `pUnkAppDomainManager` します。  
  
 メソッドの実装では、 `SetAppDomainManager` ホストはアプリケーションドメインマネージャーのアセンブリ名と型を設定できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.AppDomain>
- <xref:System.AppDomainManager>
- [IHostControl インターフェイス](ihostcontrol-interface.md)
