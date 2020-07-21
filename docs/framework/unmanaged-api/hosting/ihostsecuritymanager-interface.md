---
title: IHostSecurityManager インターフェイス
ms.date: 03/30/2017
api_name:
- IHostSecurityManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager
helpviewer_keywords:
- IHostSecurityManager interface [.NET Framework hosting]
ms.assetid: c3be2cbd-2d93-438b-9888-9a0251b63c03
topic_type:
- apiref
ms.openlocfilehash: 237fe23493460df77a79ba3aed9f0a809cd8aa23
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501470"
---
# <a name="ihostsecuritymanager-interface"></a>IHostSecurityManager インターフェイス
現在実行中のスレッドのセキュリティコンテキストに対するアクセスと制御を許可するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetSecurityContext メソッド](ihostsecuritymanager-getsecuritycontext-method.md)|ホストから要求された[IHostSecurityContext](ihostsecuritycontext-interface.md)を取得します。|  
|[ImpersonateLoggedOnUser メソッド](ihostsecuritymanager-impersonateloggedonuser-method.md)|現在のユーザー id の資格情報を使用して、コードの実行を要求します。|  
|[OpenThreadToken メソッド](ihostsecuritymanager-openthreadtoken-method.md)|現在のスレッドに関連付けられている随意アクセストークンを開きます。|  
|[RevertToSelf メソッド](ihostsecuritymanager-reverttoself-method.md)|現在のユーザー id の偽装を終了し、元のスレッドトークンを返します。|  
|[SetSecurityContext メソッド](ihostsecuritymanager-setsecuritycontext-method.md)|現在実行中のスレッドのセキュリティコンテキストを設定します。|  
|[SetThreadToken メソッド](ihostsecuritymanager-setthreadtoken-method.md)|現在実行中のスレッドのハンドルを設定します。|  
  
## <a name="remarks"></a>解説  
 ホストは、共通言語ランタイム (CLR) とユーザーコードの両方によって、スレッドトークンへのすべてのコードアクセスを制御できます。 また、完全なセキュリティコンテキスト情報が、制限されたコードアクセスで非同期操作またはコードポイント全体に渡されるようにすることもできます。 `IHostSecurityContext`CLR に対して非透過的なこのセキュリティコンテキスト情報をカプセル化します。  
  
 CLR は、マネージスレッドコンテキストを内部で処理します。 次のような状況で、プロセス固有のクエリが実行され `IHostSecurityManager` ます。  
  
- ファイナライザーの実行中に発生します。  
  
- クラスおよびモジュールコンストラクターの実行中。  
  
- ワーカースレッドの非同期ポイントで、 [IHostThreadPoolManager:: QueueUserWorkItem](ihostthreadpoolmanager-queueuserworkitem-method.md)メソッドを呼び出します。  
  
- I/o 完了ポートのサービス。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostSecurityContext インターフェイス](ihostsecuritycontext-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
