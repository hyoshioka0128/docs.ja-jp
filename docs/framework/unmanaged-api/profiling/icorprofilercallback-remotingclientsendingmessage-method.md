---
title: ICorProfilerCallback::RemotingClientSendingMessage メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RemotingClientSendingMessage
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RemotingClientSendingMessage
helpviewer_keywords:
- RemotingClientSendingMessage method [.NET Framework profiling]
- ICorProfilerCallback::RemotingClientSendingMessage method [.NET Framework profiling]
ms.assetid: 54d9a5a5-3877-49c1-a503-ce7c7943bc2a
topic_type:
- apiref
ms.openlocfilehash: 820a37c8ca16f4962bf1d72b1f0f404cffd92a1a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499962"
---
# <a name="icorprofilercallbackremotingclientsendingmessage-method"></a>ICorProfilerCallback::RemotingClientSendingMessage メソッド
クライアントがサーバーに要求を送信していることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RemotingClientSendingMessage(  
    [in] GUID *pCookie,  
    [in] BOOL fIsAsync);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pCookie`  
 から次の条件下で[ICorProfilerCallback:: RemotingServerReceivingMessage](icorprofilercallback-remotingserverreceivingmessage-method.md)で指定された値に対応する値。  
  
- リモート処理 GUID クッキーはアクティブです。  
  
- チャネルは、メッセージの送信に成功します。  
  
- GUID クッキーはサーバー側のプロセスでアクティブです。  
  
 これにより、リモート処理呼び出しと論理呼び出し履歴の作成を簡単に組み合わせることができます。  
  
 `fIsAsync`  
 から`true`呼び出しが非同期の場合は、それ以外の場合はとなる `false` 値。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
