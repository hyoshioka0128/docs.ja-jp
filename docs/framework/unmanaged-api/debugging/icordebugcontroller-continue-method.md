---
title: ICorDebugController::Continue メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugController.Continue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Continue
helpviewer_keywords:
- Continue method [.NET Framework debugging]
- ICorDebugController::Continue method [.NET Framework debugging]
ms.assetid: 8684cd06-ad3e-48ef-832e-15320e1f43a2
topic_type:
- apiref
ms.openlocfilehash: 0fd7dfc1a48e21abbc80692c110bee55beb68e6b
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82892865"
---
# <a name="icordebugcontrollercontinue-method"></a>ICorDebugController::Continue メソッド

[Stop メソッド](icordebugcontroller-stop-method.md)の呼び出し後に、マネージスレッドの実行を再開します。

## <a name="syntax"></a>構文

```cpp
HRESULT Continue (
    [in] BOOL fIsOutOfBand
);
```

## <a name="parameters"></a>パラメーター

`fIsOutOfBand`  
から帯域外`true`イベントから続行する場合はに設定します。それ以外の場合`false`は、をに設定します。

## <a name="remarks"></a>解説

`Continue`メソッドの`ICorDebugController::Stop`呼び出し後にプロセスを続行します。

混合モードのデバッグを実行する場合は、 `Continue`帯域外のイベントから継続している場合を除き、Win32 イベントスレッドでを呼び出さないでください。

*帯域内イベント*は、マネージイベント、またはデバッガーがプロセスのマネージ状態との対話をサポートする通常のアンマネージイベントのいずれかです。 この場合、デバッガーは、 `fOutOfBand`パラメーターがに`false`設定された状態で[ICorDebugUnmanagedCallback::D eのイベント](icordebugunmanagedcallback-debugevent-method.md)コールバックを受け取ります。

*アウトオブバンドイベント*は、イベントによってプロセスが停止されている間に、プロセスのマネージ状態との相互作用が不可能なアンマネージイベントです。 この場合、デバッガーは`ICorDebugUnmanagedCallback::DebugEvent` `fOutOfBand`パラメーターをに`true`設定してコールバックを受け取ります。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** CorDebug.idl、CorDebug.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
