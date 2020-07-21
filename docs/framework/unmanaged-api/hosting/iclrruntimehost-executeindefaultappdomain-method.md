---
title: ICLRRuntimeHost::ExecuteInDefaultAppDomain メソッド
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.ExecuteInDefaultAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::ExecuteInDefaultAppDomain
helpviewer_keywords:
- ICLRRuntimeHost::ExecuteInDefaultAppDomain method [.NET Framework hosting]
- ExecuteInDefaultAppDomain method [.NET Framework hosting]
ms.assetid: 30b5cf9a-a762-4bd4-be12-d6c1442b78b1
topic_type:
- apiref
ms.openlocfilehash: 070c52258b66dcc352f2beef81b9a0694b8301ce
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703287"
---
# <a name="iclrruntimehostexecuteindefaultappdomain-method"></a>ICLRRuntimeHost::ExecuteInDefaultAppDomain メソッド
指定したマネージアセンブリの指定した型の指定したメソッドを呼び出します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ExecuteInDefaultAppDomain (  
    [in] LPCWSTR pwzAssemblyPath,  
    [in] LPCWSTR pwzTypeName,
    [in] LPCWSTR pwzMethodName,  
    [in] LPCWSTR pwzArgument,  
    [out] DWORD *pReturnValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pwzAssemblyPath`  
 からメソッドを呼び出すを <xref:System.Reflection.Assembly> 定義するへのパス <xref:System.Type> 。  
  
 `pwzTypeName`  
 から<xref:System.Type>呼び出すメソッドを定義するの名前。  
  
 `pwzMethodName`  
 から呼び出すメソッドの名前。  
  
 `pwzArgument`  
 からメソッドに渡す文字列パラメーター。  
  
 `pReturnValue`  
 入出力呼び出されたメソッドによって返される整数値。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`ExecuteInDefaultAppDomain`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドから E_FAIL が返された場合、その CRL はプロセス内で使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 呼び出されたメソッドには、次のシグネチャが必要です。  
  
```cpp  
static int pwzMethodName (String pwzArgument)  
```  
  
 は `pwzMethodName` 呼び出されたメソッドの名前を表し、は `pwzArgument` そのメソッドにパラメーターとして渡される文字列値を表します。 HRESULT 値が S_OK に設定されている場合、は、呼び出された `pReturnValue` メソッドによって返される整数値に設定されます。 それ以外の場合、 `pReturnValue` は設定されません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)
