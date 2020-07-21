---
title: ICLRGCManager::GetStats メソッド
ms.date: 03/30/2017
api_name:
- ICLRGCManager.GetStats
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager::GetStats
helpviewer_keywords:
- GetStats method, ICLRGCManager interface [.NET Framework hosting]
- ICLRGCManager::GetStats method [.NET Framework hosting]
ms.assetid: ce259d1d-cd81-4490-a7a1-0d0ea0804872
topic_type:
- apiref
ms.openlocfilehash: 8622920a81f4b469361ffa879f7a4eeda697cab9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504226"
---
# <a name="iclrgcmanagergetstats-method"></a>ICLRGCManager::GetStats メソッド
共通言語ランタイムのガベージコレクションシステムに関する現在の統計のセットを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetStats (  
    [in, out] COR_GC_STATS *pStats  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pStats`  
 [入力、出力]要求された統計情報を含む[COR_GC_STATS](cor-gc-stats-structure.md)インスタンス。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`GetStats`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 CLR は、のフィールドによって指定された統計のみを計算して返し `Flags` `pStats` ます。  
  
 フィールドを `Flags` [COR_GC_STAT_TYPES](cor-gc-stat-types-enumeration.md)列挙体の1つ以上の値に設定して、 [COR_GC_STATS](cor-gc-stats-structure.md)構造内のどの統計情報を設定するかを指定します。  
  
 使用例を次に示します。  
  
```cpp  
COR_GC_STATS GCStats;  
GCStats.Flags = COR_GC_COUNTS | COR_GC_MEMORYUSAGE;  
pCLRGCManager->GetStats(&GCStats);  
```  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [自動メモリ管理](../../../standard/automatic-memory-management.md)
- [COR_GC_STATS 構造体](cor-gc-stats-structure.md)
- [COR_GC_STAT_TYPES 列挙体](cor-gc-stat-types-enumeration.md)
- [ガベージ コレクション](../../../standard/garbage-collection/index.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRGCManager インターフェイス](iclrgcmanager-interface.md)
- [CLR ホスト インターフェイス](clr-hosting-interfaces.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
