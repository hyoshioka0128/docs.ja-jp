---
title: ICLROnEventManager インターフェイス
ms.date: 03/30/2017
api_name:
- ICLROnEventManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLROnEventManager
helpviewer_keywords:
- ICLROnEventManager interface [.NET Framework hosting]
ms.assetid: 9e15a0c1-8ab6-43d0-ae28-6ec7a4edd913
topic_type:
- apiref
ms.openlocfilehash: 30312e6e09535cee2968b1f9e8ac87b461c5ff40
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703522"
---
# <a name="iclroneventmanager-interface"></a>ICLROnEventManager インターフェイス
ホストが共通言語ランタイム (CLR) イベントのコールバックを登録および登録解除できるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[RegisterActionOnEvent メソッド](iclroneventmanager-registeractiononevent-method.md)|指定されたイベントのコールバックポインターを登録します。|  
|[UnregisterActionOnEvent メソッド](iclroneventmanager-unregisteractiononevent-method.md)|指定されたイベントに対して、以前に登録されたコールバックポインターの登録を解除します。|  
  
## <a name="remarks"></a>解説  
 イベントコールバックの登録と登録解除を行うために、ホストは `ICLROnEventManager` [ICLRControl:: GetCLRManager](iclrcontrol-getclrmanager-method.md)メソッドを呼び出すことによってへの参照を取得します。  
  
> [!NOTE]
> [Eclrevent](eclrevent-enumeration.md)によって説明されているイベントは、異なるスレッドから、または CLR のアンロードまたは無効化を通知するために、複数回発生する可能性があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrEvent 列挙型](eclrevent-enumeration.md)
- [IActionOnCLREvent インターフェイス](iactiononclrevent-interface.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
