---
title: ICorDebugThread::SetDebugState メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread.SetDebugState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::SetDebugState
helpviewer_keywords:
- ICorDebugThread::SetDebugState method [.NET Framework debugging]
- SetDebugState method [.NET Framework debugging]
ms.assetid: 6382bdf6-d488-4952-b653-cb09b6e1c6c2
topic_type:
- apiref
ms.openlocfilehash: 05ae2791ee7f8bd31be38ec4d2117ddc3c2ea2bc
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83377944"
---
# <a name="icordebugthreadsetdebugstate-method"></a>ICorDebugThread::SetDebugState メソッド
このスレッドのデバッグ状態を記述するフラグを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetDebugState (  
    [in] CorDebugThreadState state  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `state`  
 からこのスレッドのデバッグ状態を指定する CorDebugThreadState 列挙値のビットごとの組み合わせ。  
  
## <a name="remarks"></a>Remarks  
 `SetDebugState`スレッドの現在のデバッグ状態を設定します。 ("現在のデバッグ状態" は、プロセスが継続されていて、実際の現在の状態ではない場合は、デバッグ状態を表します)。この場合の通常の値は THREAD_RUN です。 デバッガーだけが、スレッドのデバッグ状態に影響を与える可能性があります。 デバッグ状態は最後まで継続して実行されるので、スレッド THREAD_SUSPENDed を複数回継続したままにする場合は、1回設定するだけで、それ以降は心配する必要はありません。 スレッドを中断してプロセスを再開するとデッドロックが発生する可能性がありますが、通常はそうではありません。 これは、スレッドとプロセスの組み込みの品質であり、設計によるものです。 デバッガーは、非同期的にスレッドを中断して再開し、デッドロックを解除することができます。 スレッドのユーザー状態に USER_UNSAFE_POINT が含まれている場合、スレッドはガベージコレクション (GC) をブロックする可能性があります。 これは、中断されたスレッドがデッドロックの原因となる可能性が非常に高いことを意味します。 これは、既にキューに登録されているデバッグイベントには影響しません。 したがって、デバッガーは、スレッドを中断または再開する前に、イベントキュー全体 ( [HasQueuedCallbacks::](icordebugcontroller-hasqueuedcallbacks-method.md)を呼び出すことによって) をドレインする必要があります。 それ以外の場合は、既に中断されていると思われるスレッドでイベントを取得することがあります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
