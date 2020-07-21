---
title: IGCHost2 インターフェイス
ms.date: 03/30/2017
api_name:
- IGCHost2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IGCHost2
helpviewer_keywords:
- IGCHost2 interface [.NET Framework hosting]
ms.assetid: e5323fa4-18ac-424d-859d-a65a550d08d9
topic_type:
- apiref
ms.openlocfilehash: 976673a0caab4e041cc80e5536544c195fcf692a
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83805178"
---
# <a name="igchost2-interface"></a>IGCHost2 インターフェイス
ガベージコレクションシステムに関する情報を取得し、ガベージコレクションのいくつかの側面を制御するためのメソッドを提供します。  
  
> [!NOTE]
> 新しい開発では、代わりに[ICLRGCManager2](iclrgcmanager2-interface.md)インターフェイスを使用することをお勧めします。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[SetGCStartupLimitsEx メソッド](igchost2-setgcstartuplimitsex-method.md)|ジェネレーション0のセグメントサイズと最大サイズを設定します。 より大きいジェネレーション0およびセグメントサイズを有効に `DWORD` します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** GCHost、GCHost  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト インターフェイス](hosting-interfaces.md)
- [CLR ホスト インターフェイス](clr-hosting-interfaces.md)
- [CorRuntimeHost コクラス](corruntimehost-coclass.md)
