---
title: IHostThreadPoolManager::QueueUserWorkItem メソッド
ms.date: 03/30/2017
api_name:
- IHostThreadPoolManager.QueueUserWorkItem
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostThreadPoolManager::QueueUserWorkItem
helpviewer_keywords:
- IHostThreadPoolManager::QueueUserWorkItem method [.NET Framework hosting]
- QueueUserWorkItem method [.NET Framework hosting]
ms.assetid: 41602053-8670-4827-9d61-cbfcba509b9c
topic_type:
- apiref
ms.openlocfilehash: b3d77e30cd48310c392d38dc29f62fab565c8b42
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842466"
---
# <a name="ihostthreadpoolmanagerqueueuserworkitem-method"></a>IHostThreadPoolManager::QueueUserWorkItem メソッド
実行する関数をキューに配置し、その関数によって使用されるデータを格納しているオブジェクトを指定します。 関数は、スレッドが使用可能になったときに実行されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT QueueUserWorkItem (  
    [in] LPTHREAD_START_ROUTINE Function,  
    [in] PVOID Context,  
    [in] ULONG Flags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `Function`  
 から実行する関数を表す関数ポインター。  
  
 `Context`  
 からによって使用されるデータを格納しているオブジェクト `Function` 。  
  
 `Flags`  
 からWin32 メソッドに対して定義されている、実行を制御するフラグ値の1つ `QueueUserWorkItem` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`QueueUserWorkItem`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>コメント  
 `QueueUserWorkItem`スレッドプール内のワーカースレッドに作業項目をキューします。 そのシグネチャとパラメーターの型は、同じ名前を持つ対応する Win32 関数と同じです。 詳細については、Windows プラットフォームのドキュメントを参照してください。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>
- <xref:System.Threading.ThreadPool>
- [IHostThreadPoolManager インターフェイス](ihostthreadpoolmanager-interface.md)
