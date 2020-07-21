---
title: ICorDebugProcess3::SetEnableCustomNotification メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess3.SetEnableCustomNotification Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess3::SetEnableCustomNotification
helpviewer_keywords:
- ICorDebugProcess3::SetEnableCustomNotification method [.NET Framework debugging]
- SetEnableCustomNotification method [.NET Framework debugging]
ms.assetid: afd88ee9-2589-4461-a75a-9b6fe55a2525
topic_type:
- apiref
ms.openlocfilehash: 523d9665ffd2637a0e856d74d4d3b3838cb5e83c
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212127"
---
# <a name="icordebugprocess3setenablecustomnotification-method"></a>ICorDebugProcess3::SetEnableCustomNotification メソッド
指定された型のカスタムデバッガー通知を有効または無効にします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetEnableCustomNotification(ICorDebugClass * pClass,  
                                    BOOL fEnable);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pClass`  
 からカスタムデバッガー通知を指定する型。  
  
 `fEnable`  
 [入力] `true`カスタムデバッガー通知を有効にするには`false`通知を無効にするには 既定値は `false` です。  
  
## <a name="remarks"></a>Remarks  
 `fEnable`がに設定されている場合 `true` 、メソッドの呼び出しに <xref:System.Diagnostics.Debugger.NotifyOfCrossThreadDependency%2A?displayProperty=nameWithType> よって[ICorDebugManagedCallback3:: customnotification](icordebugmanagedcallback3-customnotification-method.md)コールバックがトリガーされます。 既定では、通知は無効になっています。そのため、デバッガーは、認識している通知の種類を指定し、処理を希望する必要があります。 このクラス[のクラスはアプリケーション](icordebug-interface.md)ドメインによってスコープが設定されているため、 `SetEnableCustomNotification` プロセス全体で通知を受け取る場合は、プロセス内のすべてのアプリケーションドメインに対してを呼び出す必要があります。  
  
 .NET Framework 4 以降、サポートされている通知は、スレッド間の依存関係通知だけです。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugProcess3 インターフェイス](icordebugprocess3-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
