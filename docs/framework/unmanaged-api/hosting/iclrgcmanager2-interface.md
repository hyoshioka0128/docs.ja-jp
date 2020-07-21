---
title: ICLRGCManager2 インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRGCManager2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager2
helpviewer_keywords:
- ICLRGCManager2 interface [.NET Framework hosting]
ms.assetid: 4b5ffd7b-9ad7-41cd-9bba-34030ae3da7e
topic_type:
- apiref
ms.openlocfilehash: 0f3ecc0d497eaee937647df47ba0956335a2fe41
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703951"
---
# <a name="iclrgcmanager2-interface"></a>ICLRGCManager2 インターフェイス
ホストが共通言語ランタイムのガベージコレクションシステムと対話できるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[SetGCStartupLimitsEx メソッド](iclrgcmanager2-setgcstartuplimitsex-method.md)|ガベージコレクションセグメントのサイズとガベージコレクションシステムのジェネレーション0の最大サイズを設定します。 より大きいジェネレーション0およびセグメントサイズを有効に `DWORD` します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスは、 [ICLRGCManager インターフェイス](iclrgcmanager-interface.md)から継承されます。  
  
 共通言語ランタイム (CLR) は、マネージ型を使用してガベージコレクション機構を実装し <xref:System.GC> ます。 ガベージコレクションシステムの詳細については、「[ガベージコレクション](../../../standard/garbage-collection/index.md)」を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [自動メモリ管理](../../../standard/automatic-memory-management.md)
- [COR_GC_STATS 構造体](cor-gc-stats-structure.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [.NET Framework 4 および 4.5 で追加された CLR ホスト インターフェイス](clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
