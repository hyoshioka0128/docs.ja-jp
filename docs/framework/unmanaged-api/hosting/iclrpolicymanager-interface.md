---
title: ICLRPolicyManager インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager
helpviewer_keywords:
- ICLRPolicyManager interface [.NET Framework hosting]
ms.assetid: 5c834aa1-f2db-408a-b230-c7bec093d364
topic_type:
- apiref
ms.openlocfilehash: 631301a10aee96bb00aeda6b0b8695f0aea186a8
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703479"
---
# <a name="iclrpolicymanager-interface"></a>ICLRPolicyManager インターフェイス
エラーやタイムアウトが発生した場合に実行されるポリシーアクションをホストが指定できるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[SetActionOnFailure メソッド](iclrpolicymanager-setactiononfailure-method.md)|指定したエラーが発生したときに共通言語ランタイム (CLR) が実行するポリシーアクションを指定します。|  
|[SetActionOnTimeout メソッド](iclrpolicymanager-setactionontimeout-method.md)|指定された操作がタイムアウトしたときに CLR が実行するポリシーアクションを指定します。|  
|[SetDefaultAction メソッド](iclrpolicymanager-setdefaultaction-method.md)|指定された操作が発生したときに CLR が実行するポリシーアクションを指定します。|  
|[SetTimeout メソッド](iclrpolicymanager-settimeout-method.md)|指定された操作のタイムアウト値を設定します。|  
|[SetTimeoutAndAction メソッド](iclrpolicymanager-settimeoutandaction-method.md)|指定された操作のタイムアウト値を設定し、操作が発生したときに CLR が実行する必要があるポリシーアクションを指定します。|  
|[SetUnhandledExceptionPolicy メソッド](iclrpolicymanager-setunhandledexceptionpolicy-method.md)|未処理の例外が発生した場合の CLR の動作を指定します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrFailure 列挙型](eclrfailure-enumeration.md)
- [EClrOperation 列挙型](eclroperation-enumeration.md)
- [EPolicyAction 列挙型](epolicyaction-enumeration.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
