---
title: ICorDebugManagedCallback::LogSwitch メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.LogSwitch
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::LogSwitch
helpviewer_keywords:
- LogSwitch method [.NET Framework debugging]
- ICorDebugManagedCallback::LogSwitch method [.NET Framework debugging]
ms.assetid: 0ac59d27-783f-4a87-b7a8-baa3ccc54582
topic_type:
- apiref
ms.openlocfilehash: f095bc0272e0e6f16467b9758d5e392d371139dd
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212686"
---
# <a name="icordebugmanagedcallbacklogswitch-method"></a>ICorDebugManagedCallback::LogSwitch メソッド
共通言語ランタイム (CLR) マネージスレッドが、 <xref:System.Diagnostics.Switch> デバッグ/トレーススイッチを作成、変更、または削除するために、クラスのメソッドを呼び出したことをデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LogSwitch (  
    [in] ICorDebugAppDomain  *pAppDomain,  
    [in] ICorDebugThread     *pThread,  
    [in] LONG                 lLevel,  
    [in] ULONG                ulReason,  
    [in] WCHAR               *pLogSwitchName,  
    [in] WCHAR               *pParentName);  
```  
  
## <a name="parameters"></a>パラメーター  
 `PAppDomain`  
 からデバッグ/トレーススイッチを作成、変更、または削除したマネージスレッドを含むアプリケーションドメインを表す、コードのオブジェクトへのポインター。  
  
 `pThread`  
 からマネージスレッドを表す、コードスレッドオブジェクトへのポインター。  
  
 `lLevel`  
 からイベントログに書き込まれた説明メッセージの重大度レベルを示す値。  
  
 `ulReason`  
 からデバッグ/トレーススイッチで実行された操作を示す[Logswitchcallreason](logswitchcallreason-enumeration.md)列挙体の値。  
  
 `pLogSwitchName`  
 からデバッグ/トレーススイッチの名前へのポインター。  
  
 `pParentName`  
 からデバッグ/トレーススイッチの親の名前へのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
