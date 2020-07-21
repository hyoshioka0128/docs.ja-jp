---
title: IHostIoCompletionManager::Bind メソッド
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.Bind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::Bind
helpviewer_keywords:
- IHostIoCompletionManager::Bind method [.NET Framework hosting]
- Bind method [.NET Framework hosting]
ms.assetid: acd74cb5-7e22-4a07-83c3-82288e1abd9f
topic_type:
- apiref
ms.openlocfilehash: 8d18e6c1dca7f52b17c19f4638410a08866905f7
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804795"
---
# <a name="ihostiocompletionmanagerbind-method"></a>IHostIoCompletionManager::Bind メソッド
以前に[CreateIoCompletionPort](ihostiocompletionmanager-createiocompletionport-method.md)を呼び出したときに作成された i/o 完了ポートに、指定されたハンドルをバインドします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Bind (  
    [in] HANDLE hPort,  
    [in] HANDLE hHandle  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `hPort`  
 からバインド先の i/o 完了ポート `hHandle` 。 の値 `hPort` が null の場合、 `hHandle` は既定の i/o 完了ポートにバインドされます。  
  
 `hHandle`  
 からバインド先のオペレーティングシステムハンドル `hPort` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`Bind`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 I/o 完了ポートは、の呼び出しを使用して作成され `CreateIoCompletionPort` ます。 CLR はを呼び出し `Bind` て、そのポートにハンドルをバインドします。  
  
> [!NOTE]
> I/o 要求が完了すると、ホストは[Iclriocomplete manager:: OnComplete](iclriocompletionmanager-oncomplete-method.md)メソッドを呼び出す必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRIoCompletionManager インターフェイス](iclriocompletionmanager-interface.md)
