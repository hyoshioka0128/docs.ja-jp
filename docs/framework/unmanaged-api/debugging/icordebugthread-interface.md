---
title: ICorDebugThread インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugThread
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread
helpviewer_keywords:
- ICorDebugThread interface [.NET Framework debugging]
ms.assetid: 3930fd9b-2bc3-4b72-80a0-b6eeb94d60c6
topic_type:
- apiref
ms.openlocfilehash: edcc0ebcadc1bd95574b0276bfd0e2d42e5474fd
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379819"
---
# <a name="icordebugthread-interface"></a>ICorDebugThread インターフェイス
プロセス内のスレッドを表します。 `ICorDebugThread` インスタンスの有効期間は、それが表しているスレッドの有効期間と同じです。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ClearCurrentException メソッド](icordebugthread-clearcurrentexception-method.md)|このメソッドは実装されていません。 使用しないでください。|  
|[CreateEval メソッド](icordebugthread-createeval-method.md)|このを操作する、のオブジェクトを作成し `ICorDebugThread` ます。|  
|[CreateStepper メソッド](icordebugthread-createstepper-method.md)|こののアクティブなフレームをステップ実行できるようにする ICorDebugStepper オブジェクトを作成し `ICorDebugThread` ます。|  
|[EnumerateChains メソッド](icordebugthread-enumeratechains-method.md)|この内のすべてのスタックチェーンを格納している ICorDebugChainEnum 列挙子へのインターフェイスポインターを取得し `ICorDebugThread` ます。|  
|[GetActiveChain メソッド](icordebugthread-getactivechain-method.md)|こののアクティブなツールチェーンへのインターフェイスポインターを取得し `ICorDebugThread` ます。|  
|[GetActiveFrame メソッド](icordebugthread-getactiveframe-method.md)|この上のアクティブなテキストフレームへのインターフェイスポインターを取得し `ICorDebugThread` ます。|  
|[GetAppDomain メソッド](icordebugthread-getappdomain-method.md)|このが現在実行されているアプリケーションドメインへのインターフェイスポインターを取得し `ICorDebugThread` ます。|  
|[GetCurrentException メソッド](icordebugthread-getcurrentexception-method.md)|現在マネージコードによってスローされている例外を表す、ICorDebugValue オブジェクトへのインターフェイスポインターを取得します。|  
|[GetDebugState メソッド](icordebugthread-getdebugstate-method.md)|このの現在のデバッグ状態を示す CorDebugThreadState 値を取得し `ICorDebugThread` ます。|  
|[GetHandle メソッド](icordebugthread-gethandle-method.md)|こののアクティブな部分の現在のハンドルを取得し `ICorDebugThread` ます。|  
|[GetID メソッド](icordebugthread-getid-method.md)|こののアクティブな部分の現在のオペレーティングシステム識別子を取得し `ICorDebugThread` ます。|  
|[GetObject メソッド](icordebugthread-getobject-method.md)|共通言語ランタイム (CLR) スレッドへのインターフェイスポインターを取得します。|  
|[GetProcess メソッド](icordebugthread-getprocess-method.md)|このがパートを形成するプロセスへのインターフェイスポインターを取得し `ICorDebugThread` ます。|  
|[GetRegisterSet メソッド](icordebugthread-getregisterset-method.md)|このに関連付けられているレジスタセットへのインターフェイスポインターを取得し `ICorDebugThread` ます。|  
|[GetUserState メソッド](icordebugthread-getuserstate-method.md)|このの現在の状態を示す CorDebugUserState 値のビットごとの組み合わせを取得し `ICorDebugThread` ます。|  
|[SetDebugState メソッド](icordebugthread-setdebugstate-method.md)|こののデバッグ状態を記述する値のビットごとの組み合わせを設定 `CorDebugThreadState` `ICorDebugThread` します。|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
