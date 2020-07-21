---
title: ICorDebugProcess::GetHelperThreadID メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetHelperThreadID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetHelperThreadID
helpviewer_keywords:
- GetHelperThreadID method [.NET Framework debugging]
- ICorDebugProcess::GetHelperThreadID method [.NET Framework debugging]
ms.assetid: 84e1e605-37c1-49a5-8e12-35db85654622
topic_type:
- apiref
ms.openlocfilehash: fc4f4b56552c4db265d2ea123a84c7792ad53094
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213635"
---
# <a name="icordebugprocessgethelperthreadid-method"></a>ICorDebugProcess::GetHelperThreadID メソッド
デバッガーの内部ヘルパースレッドのオペレーティングシステム (OS) スレッド ID を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetHelperThreadID (  
    [out] DWORD *pThreadID  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pThreadID`  
 入出力デバッガーの内部ヘルパースレッドの OS スレッド ID へのポインター。  
  
## <a name="remarks"></a>Remarks  
 マネージデバッグおよびアンマネージデバッグ中は、デバッガーによって設定されたブレークポイントにヒットした場合に、指定した ID を持つスレッドが実行された状態を維持する必要があります。 デバッガーでは、このスレッドをユーザーに対して非表示にすることもできます。 まだプロセスにヘルパースレッドが存在しない場合、 `GetHelperThreadID` メソッドは * で0を返し `pThreadID` ます。  
  
 ヘルパースレッドのスレッド ID は、時間の経過と共に変更される可能性があるため、キャッシュすることはできません。 停止イベントが発生するたびにスレッド ID を再照会する必要があります。  
  
 デバッガーのヘルパースレッドのスレッド ID は、すべてのアンマネージコードに対して、すべてのアンマネージ[コールバック:: CreateThread](icordebugmanagedcallback-createthread-method.md)イベントに対して適切になります。これにより、デバッガーはヘルパースレッドのスレッド id を判断し、ユーザーに対して非表示にすることができます。 アンマネージイベント中にヘルパースレッドとして識別されたスレッド `ICorDebugManagedCallback::CreateThread` は、マネージユーザーコードを実行しません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug。 CorDebug. h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
