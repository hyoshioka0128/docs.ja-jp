---
title: IDebuggerThreadControl::ThreadIsBlockingForDebugger メソッド
ms.date: 03/30/2017
api_name:
- IDebuggerThreadControl.ThreadIsBlockingForDebugger
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ThreadIsBlockingForDebugger
helpviewer_keywords:
- ThreadIsBlockingForDebugger method [.NET Framework hosting]
- IDebuggerThreadControl::ThreadIsBlockingForDebugger method [.NET Framework hosting]
ms.assetid: d4d7cb2d-69da-48b3-879a-1a8a68c9bfa8
topic_type:
- apiref
ms.openlocfilehash: f7cdc3fe9d52db56d0280bc602d3a9f2f54e8246
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83805252"
---
# <a name="idebuggerthreadcontrolthreadisblockingfordebugger-method"></a>IDebuggerThreadControl::ThreadIsBlockingForDebugger メソッド
このコールバックを送信しているスレッドがデバッグサービス内でブロックされようとしていることをホストに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ThreadIsBlockingForDebugger ( );  
```  
  
## <a name="remarks"></a>解説  
 `ThreadIsBlockingForDebugger`メソッドは常にランタイムスレッドで呼び出されます。  
  
 メソッドは、 `ThreadIsBlockingForDebugger` スレッドがブロックされている間に、ホストに別のアクションを実行する機会を与えます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.Net Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IDebuggerThreadControl インターフェイス](idebuggerthreadcontrol-interface.md)
