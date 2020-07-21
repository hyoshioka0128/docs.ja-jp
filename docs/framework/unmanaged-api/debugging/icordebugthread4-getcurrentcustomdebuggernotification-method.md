---
title: ICorDebugThread4::GetCurrentCustomDebuggerNotification メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread4.GetCurrentCustomDebuggerNotification Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread4::GetCurrentCustomDebuggerNotification
helpviewer_keywords:
- GetCurrentCustomDebuggerNotification method [.NET Framework debugging]
- ICorDebugThread4::GetCurrentCustomDebuggerNotification method [.NET Framework debugging]
ms.assetid: 57e0f2d2-5f0e-4e2d-99ec-3f26632eb693
topic_type:
- apiref
ms.openlocfilehash: 76ad1c0ac421f05cf30f6d3d1f3e65848796a0c7
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378696"
---
# <a name="icordebugthread4getcurrentcustomdebuggernotification-method"></a>ICorDebugThread4::GetCurrentCustomDebuggerNotification メソッド

現在のスレッドの現在の[ICorDebugManagedCallback3:: CustomNotification](icordebugmanagedcallback3-customnotification-method.md)オブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCurrentCustomDebuggerNotification(
    [out] ICorDebugValue **ppNotificationObject
    );
```

## <a name="parameters"></a>パラメーター

`ppNotificationObject`\
入出力現在のスレッド上の現在のオブジェクトへのポインター `ICorDebugManagedCallback3::CustomNotification` 。

## <a name="remarks"></a>Remarks

`ppNotificationObject`コールバック内からメソッドが呼び出されていない場合 `ICorDebugManagedCallback3::CustomNotification` 、または現在の通知オブジェクトが存在しない場合は、の値が null になります。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** CorDebug.idl、CorDebug.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]

## <a name="see-also"></a>関連項目

- [ICorDebugThread4 インターフェイス](icordebugthread4-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
