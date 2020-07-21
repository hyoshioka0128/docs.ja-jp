---
title: ICLRGCManager::SetGCStartupLimits メソッド
ms.date: 03/30/2017
api_name:
- ICLRGCManager.SetGCStartupLimits
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager::SetGCStartupLimits
helpviewer_keywords:
- SetGCStartupLimits method, ICLRGCManager interface [.NET Framework hosting]
- ICLRGCManager::SetGCStartupLimits method [.NET Framework hosting]
ms.assetid: 1c8d9959-95b5-4131-be4a-556d97774014
topic_type:
- apiref
ms.openlocfilehash: 0dce86a12ed3e93983ee62620fa0ddf7dfbc48f5
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616945"
---
# <a name="iclrgcmanagersetgcstartuplimits-method"></a>ICLRGCManager::SetGCStartupLimits メソッド
ガベージコレクションセグメントのサイズとガベージコレクションシステムのジェネレーション0の最大サイズを設定します。  
  
> [!IMPORTANT]
> .NET Framework 4.5 以降では、 `DWORD` [ICLRGCManager2:: SetGCStartupLimitsEx](iclrgcmanager2-setgcstartuplimitsex-method.md)メソッドを使用して、セグメントサイズと最大ジェネレーション0のサイズをより大きい値に設定できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetGCStartupLimits (  
    [in] DWORD SegmentSize,
    [in] DWORD MaxGen0Size  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `SegmentSize`  
 からガベージコレクションセグメントの指定されたサイズ。  
  
 セグメントの最小サイズは 4 MB です。 セグメントは、1 MB 以上の単位で増やすことができます。  
  
 `MaxGen0Size`  
 からジェネレーション0の指定された最大サイズ。  
  
 ジェネレーション0の最小サイズは 64 KB です。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetGCStartupLimits`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 を設定する値は、 `SetGCStartupLimits` 1 回だけ指定できます。 の後の呼び出し `SetGCStartupLimits` は無視されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [自動メモリ管理](../../../standard/automatic-memory-management.md)
- [ガベージ コレクション](../../../standard/garbage-collection/index.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRGCManager インターフェイス](iclrgcmanager-interface.md)
