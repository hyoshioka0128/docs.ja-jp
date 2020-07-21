---
title: ICLRPolicyManager::SetActionOnFailure メソッド
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager.SetActionOnFailure
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager::SetActionOnFailure
helpviewer_keywords:
- SetActionOnFailure method [.NET Framework hosting]
- ICLRPolicyManager::SetActionOnFailure method [.NET Framework hosting]
ms.assetid: 4664033f-db97-4388-b988-2ec470796e58
topic_type:
- apiref
ms.openlocfilehash: 727cd82226b9a59c4879ffea5e87f93dd5fe38c9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504109"
---
# <a name="iclrpolicymanagersetactiononfailure-method"></a>ICLRPolicyManager::SetActionOnFailure メソッド
指定したエラーが発生したときに共通言語ランタイム (CLR) が実行するポリシーアクションを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetActionOnFailure (  
    [in] EClrFailure   failure,  
    [in] EPolicyAction action  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `failure`  
 から[Eclrfailure](eclrfailure-enumeration.md)値の1つで、アクションを実行するエラーの種類を示します。  
  
 `action`  
 から[Epolicyaction](epolicyaction-enumeration.md)値の1つ。エラーが発生したときに実行するアクションを示します。 サポートされている値の一覧については、「解説」を参照してください。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetActionOnFailure`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_INVALIDARG|指定された操作に対してポリシーアクションを設定できないか、操作に無効なポリシーアクションが指定されました。|  
  
## <a name="remarks"></a>解説  
 既定では、メモリなどのリソースの割り当てに失敗した場合、CLR は例外をスローします。 `SetActionOnFailure`エラー発生時に実行するポリシーアクションを指定して、ホストがこの動作をオーバーライドできるようにします。 次の表は、サポートされている[Eclrfailure](eclrfailure-enumeration.md)値と[epolicyaction](epolicyaction-enumeration.md)値の組み合わせを示しています。 (FAIL_ プレフィックスは[Eclrfailure](eclrfailure-enumeration.md)値から省略されています)。  
  
||NonCriticalResource|CriticalResource|Fat (Alruntime)|OrphanedLock|StackOverflow|AccessViolation|CodeContract|  
|-|-------------------------|----------------------|------------------|------------------|-------------------|---------------------|------------------|  
|`eNoAction`|X|X||||該当なし||  
|の例外|X|X||||該当なし||  
|`eAbortThread`|X|X||||該当なし|X|  
|`eRudeAbortThread`|X|X||||該当なし|X|  
|`eUnloadAppDomain`|X|X||X||該当なし|X|  
|`eRudeUnloadAppDomain`|X|X||X|X|該当なし|X|  
|`eExitProcess`|X|X||X|X|該当なし|X|  
|eFastExitProcess|X|X||X|X|該当なし||  
|`eRudeExitProcess`|X|X|X|X|X|該当なし||  
|`eDisableRuntime`|X|X|X|X|X|該当なし||  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrFailure 列挙型](eclrfailure-enumeration.md)
- [EPolicyAction 列挙型](epolicyaction-enumeration.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
