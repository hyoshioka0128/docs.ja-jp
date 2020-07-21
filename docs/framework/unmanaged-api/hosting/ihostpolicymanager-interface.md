---
title: IHostPolicyManager インターフェイス
ms.date: 03/30/2017
api_name:
- IHostPolicyManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostPolicyManager
helpviewer_keywords:
- IHostPolicyManager interface [.NET Framework hosting]
ms.assetid: 8c4aa124-5e00-46d9-b1e8-57ba6574bb0d
topic_type:
- apiref
ms.openlocfilehash: d6b34403a45cc40863d79b59396041e496989045
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503940"
---
# <a name="ihostpolicymanager-interface"></a>IHostPolicyManager インターフェイス
中止、タイムアウト、またはエラーが発生した場合に共通言語ランタイム (CLR) が実行するアクションをホストに通知するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[OnDefaultAction メソッド](ihostpolicymanager-ondefaultaction-method.md)|CLR が、スレッドの中止またはアンロードに応答して[ICLRPolicyManager:: SetDefaultAction](iclrpolicymanager-setdefaultaction-method.md)の呼び出しによって指定された既定のアクションを実行しようとしていることをホストに通知し <xref:System.AppDomain> ます。|  
|[OnFailure メソッド](ihostpolicymanager-onfailure-method.md)|リソース割り当てまたは再利用エラーに応答して、CLR が[ICLRPolicyManager:: SetActionOnFailure](iclrpolicymanager-setactiononfailure-method.md)の呼び出しによって指定されたアクションを実行しようとしていることをホストに通知します。|  
|[OnTimeout メソッド](ihostpolicymanager-ontimeout-method.md)|タイムアウトに応答して[ICLRPolicyManager:: SetActionOnTimeout](iclrpolicymanager-setactionontimeout-method.md)への呼び出しによって指定されたアクションを CLR が実行しようとしていることをホストに通知します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrFailure 列挙型](eclrfailure-enumeration.md)
- [EClrOperation 列挙型](eclroperation-enumeration.md)
- [EPolicyAction 列挙型](epolicyaction-enumeration.md)
- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
