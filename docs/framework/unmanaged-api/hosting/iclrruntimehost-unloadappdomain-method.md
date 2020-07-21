---
title: ICLRRuntimeHost::UnloadAppDomain メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.UnloadAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::UnloadAppDomain
helpviewer_keywords:
- ICLRRuntimeHost::UnloadAppDomain method [.NET Framework hosting]
- UnloadAppDomain method [.NET Framework hosting]
ms.assetid: 571912bc-3429-4ff8-8eb2-ea993ffbd901
topic_type:
- apiref
ms.openlocfilehash: 293c1764f4c0d857138726b8ed4855b1e3b03116
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703923"
---
# <a name="iclrruntimehostunloadappdomain-method"></a>ICLRRuntimeHost::UnloadAppDomain メソッド
<xref:System.AppDomain>指定した数値識別子に対応するマネージをアンロードします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT UnloadAppDomain(  
    [in] DWORD dwAppDomainId  
    [in] BOOL  fWaitUntilDone  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwAppDomainId`  
 からアンロードするアプリケーションドメインの数値識別子。  
  
 `fWaitUntilDone`  
 [入力] `true`アプリケーションドメインのアンロードを試行する前に、共通言語ランタイム (CLR) がアプリケーションの現在のスレッドの実行を完了するまで待機する必要があることを示す場合は。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`UnloadAppDomain`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返す場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 [GetCurrentAppDomainId](iclrruntimehost-getcurrentappdomainid-method.md)を呼び出すことにより、現在のスレッドが実行されているアプリケーションドメインの数値識別子を取得できます。 この識別子は <xref:System.AppDomain.Id%2A> 、マネージ型のプロパティに対応 <xref:System.AppDomain> しています。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)
