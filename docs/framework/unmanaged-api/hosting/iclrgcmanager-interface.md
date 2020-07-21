---
title: ICLRGCManager インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRGCManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager
helpviewer_keywords:
- ICLRGCManager interface [.NET Framework hosting]
ms.assetid: fb511c9b-3fe4-41b0-822a-6ba4a079d1f5
topic_type:
- apiref
ms.openlocfilehash: f878e2f1f86bc42c0ff5abada8d7df4feb9ed228
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504194"
---
# <a name="iclrgcmanager-interface"></a>ICLRGCManager インターフェイス
ホストが共通言語ランタイムのガベージコレクションシステムと対話できるようにするメソッドを提供します。  
  
> [!NOTE]
> .NET Framework 4.5 以降では、 [ICLRGCManager2:: SetGCStartupLimitsEx](iclrgcmanager2-setgcstartuplimitsex-method.md)メソッドを使用して、ガベージコレクションセグメントのサイズと、ガベージコレクションシステムのジェネレーション0の最大サイズを、 `DWORD` [SetGCStartupLimits](iclrgcmanager-setgcstartuplimits-method.md)メソッドによって設定された制限を超える値に設定できます。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Collect メソッド](iclrgcmanager-collect-method.md)|指定したジェネレーションのガベージコレクションを強制的に実行します。|  
|[GetStats メソッド](iclrgcmanager-getstats-method.md)|ガベージコレクションシステムに関する現在の統計のセットを取得します。|  
|[SetGCStartupLimits メソッド](iclrgcmanager-setgcstartuplimits-method.md)|ガベージコレクションセグメントのサイズとガベージコレクションシステムのジェネレーション0の最大サイズを設定します。|  
  
## <a name="remarks"></a>解説  
 共通言語ランタイム (CLR) は、マネージ型を使用してガベージコレクション機構を実装し <xref:System.GC> ます。 ガベージコレクションシステムの詳細については、「[ガベージコレクション](../../../standard/garbage-collection/index.md)」を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [自動メモリ管理](../../../standard/automatic-memory-management.md)
- [COR_GC_STATS 構造体](cor-gc-stats-structure.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [CLR ホスト インターフェイス](clr-hosting-interfaces.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
