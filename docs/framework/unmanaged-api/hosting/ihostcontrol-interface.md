---
title: IHostControl インターフェイス
ms.date: 03/30/2017
api_name:
- IHostControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostControl
helpviewer_keywords:
- IHostControl interface [.NET Framework hosting]
ms.assetid: a4ae0d1f-ade9-4b0a-a122-93ed11a5e6b3
topic_type:
- apiref
ms.openlocfilehash: 9dd89abb332853b966aa81dc506099b7af6ca3b2
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804930"
---
# <a name="ihostcontrol-interface"></a>IHostControl インターフェイス
アセンブリの読み込みを構成し、ホストがサポートするホストインターフェイスを決定するためのメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetHostManager メソッド](ihostcontrol-gethostmanager-method.md)|指定したを使用して、ホストのインターフェイスの実装へのインターフェイスポインターを取得し `IID` ます。|  
|[SetAppDomainManager メソッド](ihostcontrol-setappdomainmanager-method.md)|アプリケーションドメインが作成されたことをホストに通知します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.AppDomainManager>
- [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
