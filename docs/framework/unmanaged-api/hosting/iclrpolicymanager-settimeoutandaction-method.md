---
title: ICLRPolicyManager::SetTimeoutAndAction メソッド
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager.SetTimeoutAndAction
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager::SetTimeoutAndAction
helpviewer_keywords:
- ICLRPolicyManager::SetTimeoutAndAction method [.NET Framework hosting]
- SetTimeoutAndAction method [.NET Framework hosting]
ms.assetid: 60454f91-d855-4ddf-bb6d-60a02f5eabab
topic_type:
- apiref
ms.openlocfilehash: 02e836601be72d54f561e077cd3c466470bafb25
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504096"
---
# <a name="iclrpolicymanagersettimeoutandaction-method"></a>ICLRPolicyManager::SetTimeoutAndAction メソッド
指定された操作のタイムアウト値を設定し、操作が発生したときに共通言語ランタイム (CLR) が実行するポリシーアクションを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetTimeoutAndAction (  
    [in] EClrOperation operation,  
    [in] DWORD dwMilliseconds,  
    [in] EPolicyAction action  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `operation`  
 からタイムアウトとポリシーを設定する操作を示す[EClrOperation](eclroperation-enumeration.md)値の1つ `action` 。 サポートされている値を次に示します。  
  
- OPR_AppDomainUnload  
  
- OPR_ProcessExit  
  
- OPR_ThreadRudeAbortInCriticalRegion  
  
- OPR_ThreadRudeAbortInNonCriticalRegion  
  
 `dwMilliseconds`  
 から新しいタイムアウト値 (ミリ秒単位)。 値が無限であると、 `operation` タイムアウトしません。  
  
 `action`  
 から[Epolicyaction](epolicyaction-enumeration.md)値の1つ。 CLR が発生したときに実行するポリシーアクションを示し `operation` ます。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetTimeoutAndAction`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_INVALIDARG|指定されたに対してタイムアウトを設定できない `operation` か、に無効な値が指定されました `action` 。|  
  
## <a name="remarks"></a>解説  
 `SetTimeoutAndAction`[ICLRPolicyManager:: SetTimeout](iclrpolicymanager-settimeout-method.md)メソッドと[ICLRPolicyManager:: SetActionOnTimeout](iclrpolicymanager-setactionontimeout-method.md)メソッドの機能をカプセル化し、これら2つのメソッドの順次呼び出しの代わりに呼び出すことができます。  
  
> [!IMPORTANT]
> すべてのポリシーアクション値は、CLR 操作のタイムアウト動作として指定できるわけではありません。 有効な値については、これら2つの方法に関するトピックの「解説」セクションを参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrOperation 列挙型](eclroperation-enumeration.md)
- [EPolicyAction 列挙型](epolicyaction-enumeration.md)
- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
- [SetActionOnTimeout メソッド](iclrpolicymanager-setactionontimeout-method.md)
- [ICLRPolicyManager:: SetTimeoutAndAction](iclrpolicymanager-settimeoutandaction-method.md)
