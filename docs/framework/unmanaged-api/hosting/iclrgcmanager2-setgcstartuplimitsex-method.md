---
title: ICLRGCManager2::SetGCStartupLimitsEx メソッド
ms.date: 03/30/2017
api_name:
- ICLRGCManager2.SetGCStartupLimitsEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager2::SetCLRGCStartupLimitsEx
helpviewer_keywords:
- ICLRGCManager2::SetGCStartupLimitsEx method [.NET Framework hosting]
- SetGCStartupLimitsEx method, ICLRGCManager2 interface [.NET Framework hosting]
ms.assetid: 6c3a08a9-5d65-48d4-8bbf-2a86ed7d356a
topic_type:
- apiref
ms.openlocfilehash: f71c3b738d8e1f1670ac870d5e8c23ea9182d924
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703973"
---
# <a name="iclrgcmanager2setgcstartuplimitsex-method"></a>ICLRGCManager2::SetGCStartupLimitsEx メソッド
ガベージコレクションセグメントのサイズとガベージコレクションシステムのジェネレーション0の最大サイズを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetGCStartupLimitsEx (  
    [in] SIZE_T SegmentSize,
    [in] SIZE_T MaxGen0Size  
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
|S_OK|`SetGCStartupLimitsEx`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 を設定する値は、 `SetGCStartupLimitsEx` ホストを開始する前にのみ指定できます。 の後の呼び出し `SetGCStartupLimitsEx` は無視されます。  
  
 どちらか一方のパラメーターに影響を及ぼさずに設定するには、変更しないパラメーターに 0 (ゼロ) を指定します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [自動メモリ管理](../../../standard/automatic-memory-management.md)
- [ガベージ コレクション](../../../standard/garbage-collection/index.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRGCManager2 インターフェイス](iclrgcmanager2-interface.md)
