---
title: IHostSecurityContext インターフェイス
ms.date: 03/30/2017
api_name:
- IHostSecurityContext
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityContext
helpviewer_keywords:
- IHostSecurityContext interface [.NET Framework hosting]
ms.assetid: 88e2eac0-8ccb-404f-abbc-287d55159842
topic_type:
- apiref
ms.openlocfilehash: f6e25bfe11880730f6f447ccc0406d716d185624
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501496"
---
# <a name="ihostsecuritycontext-interface"></a>IHostSecurityContext インターフェイス
共通言語ランタイム (CLR) が、ホストによって実装されたセキュリティコンテキスト情報を維持できるようにします。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Capture メソッド](ihostsecuritycontext-capture-method.md)|`IHostSecurityContext` [IHostSecurityManager:: GetSecurityContext](ihostsecuritymanager-getsecuritycontext-method.md)への呼び出しから返されたインスタンスの複製を取得します。|  
  
## <a name="remarks"></a>解説  
 ホストは、CLR とユーザーコードの両方によって、スレッドトークンへのすべてのコードアクセスを制御できます。 また、完全なセキュリティコンテキスト情報が、制限されたコードアクセスで非同期操作またはコードポイント全体に渡されるようにすることもできます。 `IHostSecurityContext`このセキュリティコンテキスト情報をカプセル化します。この情報は、ランタイムに対して非透過的です。 ランタイムはを使用してこの情報をキャプチャ `Capture` し、スレッドプールのワーカー項目のディスパッチ、ファイナライザーの実行、およびモジュールコンストラクターとクラスコンストラクター間で移動します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRHostProtectionManager インターフェイス](iclrhostprotectionmanager-interface.md)
- [IHostSecurityManager インターフェイス](ihostsecuritymanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
