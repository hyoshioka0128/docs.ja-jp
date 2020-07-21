---
title: IHostPolicyManager::OnDefaultAction メソッド
ms.date: 03/30/2017
api_name:
- IHostPolicyManager.OnDefaultAction
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostPolicyManager::OnDefaultAction
helpviewer_keywords:
- OnDefaultAction method [.NET Framework hosting]
- IHostPolicyManager::OnDefaultAction method [.NET Framework hosting]
ms.assetid: 071e73bd-4795-470f-9373-cfaef553b7f2
topic_type:
- apiref
ms.openlocfilehash: e6aa8cb814e509d310c2f5b5524e0fd6727fc43f
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804284"
---
# <a name="ihostpolicymanagerondefaultaction-method"></a>IHostPolicyManager::OnDefaultAction メソッド
スレッドの中止またはアンロードに応じて、 [ICLRPolicyManager:: SetDefaultAction](iclrpolicymanager-setdefaultaction-method.md)メソッドの呼び出しによって設定された既定のアクションを共通言語ランタイム (CLR: common language runtime) が実行しようとしていることをホストに通知し <xref:System.AppDomain> ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OnDefaultAction (  
    [in] EClrOperation  operation,
    [in] EPolicyAction  action  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `operation`  
 から[EClrOperation](eclroperation-enumeration.md)値の1つ。 CLR が応答するイベントの種類を示します。  
  
 `action`  
 からイベントへの応答として CLR が実行しているアクションを示す[Epolicyaction](epolicyaction-enumeration.md)値の1つ。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`OnDefaultAction`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しを処理できません。 なく|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrOperation 列挙型](eclroperation-enumeration.md)
- [EPolicyAction 列挙型](epolicyaction-enumeration.md)
- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
- [IHostPolicyManager インターフェイス](ihostpolicymanager-interface.md)
