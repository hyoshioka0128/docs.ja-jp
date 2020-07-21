---
title: ICorProfilerCallback::RemotingClientInvocationFinished メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RemotingClientInvocationFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RemotingClientInvocationFinished
helpviewer_keywords:
- RemotingClientInvocationFinished method [.NET Framework profiling]
- ICorProfilerCallback::RemotingClientInvocationFinished method [.NET Framework profiling]
ms.assetid: ea4b283b-1210-4f41-a7a2-c398b1adde4e
topic_type:
- apiref
ms.openlocfilehash: f5786db1f17e8a463dc78f9c93464145be3a8f32
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499988"
---
# <a name="icorprofilercallbackremotingclientinvocationfinished-method"></a>ICorProfilerCallback::RemotingClientInvocationFinished メソッド
リモート処理呼び出しがクライアントで完了まで実行されたことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RemotingClientInvocationFinished();  
```  
  
## <a name="remarks"></a>解説  
 リモート処理の呼び出しが同期されている場合は、サーバー上でも完了まで実行されます。 リモート処理呼び出しが非同期の場合は、呼び出しが処理されるときに応答が必要になることがあります。 応答が予想される場合は、 [ICorProfilerCallback:: RemotingClientReceivingReply](icorprofilercallback-remotingclientreceivingreply-method.md)の呼び出しとして、および `RemotingClientInvocationFinished` 非同期呼び出しの必要なセカンダリ処理を示すための追加の呼び出しとして発生します。  
  
 次のコールバックの各ペアは、同じスレッドで実行されます。  
  
- `RemotingClientInvocationStarted`and [ICorProfilerCallback:: RemotingClientSendingMessage](icorprofilercallback-remotingclientsendingmessage-method.md)  
  
- [ICorProfilerCallback:: RemotingClientReceivingReply](icorprofilercallback-remotingclientreceivingreply-method.md)と[ICorProfilerCallback:: RemotingClientInvocationFinished](icorprofilercallback-remotingclientinvocationfinished-method.md)  
  
- [ICorProfilerCallback:: RemotingServerInvocationReturned](icorprofilercallback-remotingserverinvocationreturned-method.md)と[ICorProfilerCallback:: RemotingServerSendingReply](icorprofilercallback-remotingserversendingreply-method.md)  
  
 リモート処理のコールバックでは、次の問題に注意する必要があります。  
  
- リモート処理関数の実行はプロファイラー API によっては反映されないため、クライアントから呼び出され、サーバーで実行される関数の通知は正しく受信されません。 実際の呼び出しは、プロキシオブジェクトを介して行われます。プロファイラーには、特定の関数が JIT コンパイルされていても使用されていないように見えます。  
  
- プロファイラーは、非同期のリモート処理イベントに対して正確な通知を受信しません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
