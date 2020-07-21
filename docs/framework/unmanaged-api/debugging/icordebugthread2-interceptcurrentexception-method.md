---
title: ICorDebugThread2::InterceptCurrentException メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.InterceptCurrentException
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::InterceptCurrentException
helpviewer_keywords:
- InterceptCurrentException method [.NET Framework debugging]
- ICorDebugThread2::InterceptCurrentException method [.NET Framework debugging]
ms.assetid: 536d2357-1b97-49e0-a10c-c860aed74e6e
topic_type:
- apiref
ms.openlocfilehash: d87f07e6cadf8c9b5a4d8bb3063333c26e2c4ff1
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379031"
---
# <a name="icordebugthread2interceptcurrentexception-method"></a>ICorDebugThread2::InterceptCurrentException メソッド
デバッガーがこのスレッドの現在の例外をインターセプトできるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT InterceptCurrentException (  
    [in] ICorDebugFrame  *pFrame  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pFrame`  
 からアクティブなスタックフレームを表すテキストフレームへのポインター。  
  
## <a name="remarks"></a>Remarks  
 メソッドは、 `InterceptCurrentException` 例外コールバック ( [ICorDebugManagedCallback2:: exception](icordebugmanagedcallback2-exception-method.md)) と、それに関連付けられています: [: Continue](icordebugcontroller-continue-method.md)への呼び出しの間で呼び出すことができます。[ICorDebugManagedCallback::Exception](icordebugmanagedcallback-exception-method.md)  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
