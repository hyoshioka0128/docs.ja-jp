---
title: ICLRTask::SetTaskIdentifier メソッド
ms.date: 03/30/2017
api_name:
- ICLRTask.SetTaskIdentifier
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask::SetTaskIdentifier
helpviewer_keywords:
- SetTaskIdentifier method [.NET Framework hosting]
- ICLRTask::SetTaskIdentifier method [.NET Framework hosting]
ms.assetid: bdb7f047-1e90-40fc-9e3b-d44a16509073
topic_type:
- apiref
ms.openlocfilehash: e1b93356fd40aacdec2e764946e3e3b12d0bd306
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762943"
---
# <a name="iclrtasksettaskidentifier-method"></a>ICLRTask::SetTaskIdentifier メソッド
共通言語ランタイム (CLR) に対して、指定された識別子の値を現在の[ICLRTask](iclrtask-interface.md)インスタンスによって表されるタスクに関連付けるように指示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetTaskIdentifier (  
    [in] DWORD Asked  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `Asked`  
 から現在のインスタンスによって表されるタスクに関連付ける共通言語ランタイムの一意の識別子 `ICLRTask` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetTaskIdentifier`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 ホストは、デバッグ環境で CLR とホストを統合できるように、識別子をタスクに関連付けることができます。 この識別子は、CLR には意味がありません。 CLR はこれをデバッガーアプリケーションに渡します。 デバッガーはこの識別子を使用して、CLR 呼び出し履歴をホストの呼び出し履歴に関連付けて、デバッガーのユーザーインターフェイスに表示されたときに、それぞれのトレース情報を統合できるようにします。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRTask インターフェイス](iclrtask-interface.md)
- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)
