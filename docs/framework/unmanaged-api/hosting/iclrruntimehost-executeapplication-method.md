---
title: ICLRRuntimeHost::ExecuteApplication メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.ExecuteApplication
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::ExecuteApplication
helpviewer_keywords:
- ICLRRuntimeHost::ExecuteApplication method [.NET Framework hosting]
- ExecuteApplication method [.NET Framework hosting]
ms.assetid: 5f28cc4e-7176-4e00-aa1f-58ae6ee52fe4
topic_type:
- apiref
ms.openlocfilehash: 924d032c42dca95b253acea167d55dd6e2b811e5
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703338"
---
# <a name="iclrruntimehostexecuteapplication-method"></a>ICLRRuntimeHost::ExecuteApplication メソッド
新しいドメインでアクティブ化するアプリケーションを指定するために、マニフェストベースの ClickOnce 配置シナリオで使用されます。 これらのシナリオの詳細については、「 [ClickOnce のセキュリティと配置](/visualstudio/deployment/clickonce-security-and-deployment)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ExecuteApplication(  
    [in] LPCWSTR   pwzAppFullName,  
    [in] DWORD     dwManifestPaths,  
    [in] LPCWSTR   *ppwzManifestPaths,  
    [in] DWORD     dwActivationData,  
    [in] LPCWSTR   *ppwzActivationData,  
    [out] int      *pReturnValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzAppFullName`  
 からに定義されているアプリケーションの完全名 <xref:System.ApplicationIdentity> 。  
  
 `dwManifestPaths`  
 から配列に格納されている文字列の数 `ppwzManifestPaths` 。  
  
 `ppwzManifestPaths`  
 [in] オプション。 アプリケーションのマニフェストパスを格納する文字列配列。  
  
 `dwActivationData`  
 から配列に格納されている文字列の数 `ppwzActivationData` 。  
  
 `ppwzActivationData`  
 [in] オプション。 Web に配置されたアプリケーションの URL のクエリ文字列部分など、アプリケーションのアクティベーションデータを格納する文字列配列。  
  
 `pReturnValue`  
 入出力アプリケーションのエントリポイントから返される値。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`ExecuteApplication`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返す場合、そのプロセス内で CLR は使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 `ExecuteApplication`は、新しく作成されたアプリケーションドメインで ClickOnce アプリケーションをアクティブ化するために使用されます。  
  
 `pReturnValue`出力パラメーターは、アプリケーションによって返される値に設定されます。 に null 値を指定した場合 `pReturnValue` 、 `ExecuteApplication` は失敗しませんが、値を返しません。  
  
> [!IMPORTANT]
> メソッドを呼び出してからマニフェストベースのアプリケーションをアクティブ化する前に、 [Start メソッド](iclrruntimehost-start-method.md)メソッドを呼び出さないでください `ExecuteApplication` 。 `Start`メソッドが最初に呼び出された場合、 `ExecuteApplication` メソッドの呼び出しは失敗します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.ActivationContext>
- <xref:System.AppDomainManager>
- <xref:System.ApplicationIdentity>
- [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)
- [SetAppDomainManager メソッド](ihostcontrol-setappdomainmanager-method.md)
- [チュートリアル: デザイナーを使用して ClickOnce 配置 API で必要に応じてアセンブリをダウンロードする](/visualstudio/deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer)
