---
title: ICorConfiguration::SetGCThreadControl メソッド
ms.date: 03/30/2017
api_name:
- ICorConfiguration.SetGCThreadControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- SetGCThreadControl
helpviewer_keywords:
- ICorConfiguration::SetGCThreadControl method [.NET Framework hosting]
- SetGCThreadControl method [.NET Framework hosting]
ms.assetid: 72e38e61-3d56-4ae3-b8f6-0ab7922aaf11
topic_type:
- apiref
ms.openlocfilehash: 7874424150e0f4e1818ad9c72e31fd584e016829
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762397"
---
# <a name="icorconfigurationsetgcthreadcontrol-method"></a>ICorConfiguration::SetGCThreadControl メソッド
ガベージコレクションに対してブロックされる非ランタイムタスクのスレッドをスケジュールするためのコールバックインターフェイスを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetGCThreadControl (  
    [in] IGCThreadControl* pGCThreadControl  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pGCThreadControl`  
 から非ランタイムタスクのスレッドの中断をホストに通知する[Igcthreadcontrol](igcthreadcontrol-interface.md)オブジェクトへのポインター。  
  
## <a name="remarks"></a>解説  
 ホストは、スレッドを再スケジュールするかどうかにかかわらず、 [Igcthreadcontrol:: ThreadIsBlockingForSuspension](igcthreadcontrol-threadisblockingforsuspension-method.md)コールバック内で選択できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorConfiguration インターフェイス](icorconfiguration-interface.md)
