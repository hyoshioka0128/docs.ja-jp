---
title: ICorDebugManagedCallback インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback
helpviewer_keywords:
- ICorDebugManagedCallback interface [.NET Framework debugging]
ms.assetid: b47f1d61-c7dc-4196-b926-0b08c94f7041
topic_type:
- apiref
ms.openlocfilehash: cb2b69c5e6dfed4e0cb4e4e324c4ec6ad664f3e7
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212751"
---
# <a name="icordebugmanagedcallback-interface"></a>ICorDebugManagedCallback インターフェイス
デバッガーのコールバックを処理するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Break メソッド](icordebugmanagedcallback-break-method.md)|<xref:System.Reflection.Emit.OpCodes.Break>コードストリーム内の命令が実行されたときに、デバッガーに通知します。|  
|[Breakpoint メソッド](icordebugmanagedcallback-breakpoint-method.md)|ブレークポイントが検出されたときにデバッガーに通知します。|  
|[BreakpointSetError メソッド](icordebugmanagedcallback-breakpointseterror-method.md)|関数が just-in-time (JIT) コンパイルされる前に設定されたブレークポイントを共通言語ランタイム (CLR) が正しくバインドできなかったことをデバッガーに通知します。|  
|[ControlCTrap メソッド](icordebugmanagedcallback-controlctrap-method.md)|デバッグ中のプロセスで CTRL + C がトラップされることをデバッガーに通知します。|  
|[CreateAppDomain メソッド](icordebugmanagedcallback-createappdomain-method.md)|アプリケーションドメインが作成されたことをデバッガーに通知します。|  
|[CreateProcess メソッド](icordebugmanagedcallback-createprocess-method.md)|プロセスが初めてアタッチまたは開始されたときにデバッガーに通知します。|  
|[CreateThread メソッド](icordebugmanagedcallback-createthread-method.md)|スレッドがマネージコードの実行を開始したことをデバッガーに通知します。|  
|[DebuggerError メソッド](icordebugmanagedcallback-debuggererror-method.md)|CLR からのイベントを処理しようとしたときにエラーが発生したことをデバッガーに通知します。|  
|[EditAndContinueRemap メソッド](icordebugmanagedcallback-editandcontinueremap-method.md)|非推奨になりました。 リマップイベントが IDE に送信されたことをデバッガーに通知します。|  
|[EvalComplete メソッド](icordebugmanagedcallback-evalcomplete-method.md)|評価が完了したことをデバッガーに通知します。|  
|[EvalException メソッド](icordebugmanagedcallback-evalexception-method.md)|ハンドルされない例外で評価が終了したことをデバッガーに通知します。|  
|[Exception メソッド](icordebugmanagedcallback-exception-method.md)|マネージコードから例外がスローされたことをデバッガーに通知します。|  
|[ExitAppDomain メソッド](icordebugmanagedcallback-exitappdomain-method.md)|アプリケーションドメインが終了したことをデバッガーに通知します。|  
|[ExitProcess メソッド](icordebugmanagedcallback-exitprocess-method.md)|プロセスが終了したことをデバッガーに通知します。|  
|[ExitThread メソッド](icordebugmanagedcallback-exitthread-method.md)|マネージコードを実行していたスレッドが終了したことをデバッガーに通知します。|  
|[LoadAssembly メソッド](icordebugmanagedcallback-loadassembly-method.md)|CLR アセンブリが正常に読み込まれたことをデバッガーに通知します。|  
|[LoadClass メソッド](icordebugmanagedcallback-loadclass-method.md)|クラスが読み込まれたことをデバッガーに通知します。|  
|[LoadModule メソッド](icordebugmanagedcallback-loadmodule-method.md)|CLR モジュールが正常に読み込まれたことをデバッガーに通知します。|  
|[LogMessage メソッド](icordebugmanagedcallback-logmessage-method.md)|CLR マネージスレッドが <xref:System.Diagnostics.EventLog> イベントをログに記録するためにクラスのメソッドを呼び出したことをデバッガーに通知します。|  
|[LogSwitch メソッド](icordebugmanagedcallback-logswitch-method.md)|CLR マネージスレッドが、 <xref:System.Diagnostics.Switch> デバッグ/トレーススイッチを作成、変更、または削除するために、クラスのメソッドを呼び出したことをデバッガーに通知します。|  
|[NameChange メソッド](icordebugmanagedcallback-namechange-method.md)|アプリケーションドメインまたはスレッドの名前が変更されたことをデバッガーに通知します。|  
|[StepComplete メソッド](icordebugmanagedcallback-stepcomplete-method.md)|ステップが完了したことをデバッガーに通知します。|  
|[UnloadAssembly メソッド](icordebugmanagedcallback-unloadassembly-method.md)|CLR アセンブリがアンロードされたことをデバッガーに通知します。|  
|[UnloadClass メソッド](icordebugmanagedcallback-unloadclass-method.md)|クラスがアンロードされていることをデバッガーに通知します。|  
|[UnloadModule メソッド](icordebugmanagedcallback-unloadmodule-method.md)|CLR モジュール (DLL) がアンロードされたことをデバッガーに通知します。|  
|[UpdateModuleSymbols メソッド](icordebugmanagedcallback-updatemodulesymbols-method.md)|CLR モジュールのシンボルが変更されたことをデバッガーに通知します。|  
  
## <a name="remarks"></a>Remarks  
 すべてのコールバックがシリアル化され、同じスレッドで呼び出され、プロセスと同期された状態で呼び出されます。  
  
 各コールバックの実装では、実行を再開するために、「いいね! [:: Continue](icordebugcontroller-continue-method.md) 」を呼び出します。 `ICorDebugController::Continue`コールバックが戻る前にが呼び出されなかった場合、プロセスは停止したままになり、が呼び出されるまで、これ以上イベントコールバックは実行されません `ICorDebugController::Continue` 。  
  
 デバッガーが .NET Framework バージョン2.0 のアプリケーションをデバッグしている場合は、 [ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)を実装する必要があります。 またはのインスタンスは、 `ICorDebugManagedCallback` `ICorDebugManagedCallback2` コールバックオブジェクトとして[ICorDebug:: setmanagedhandler](icordebug-setmanagedhandler-method.md)に渡されます。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebug インターフェイス](icordebug-interface.md)
- [ICorDebugManagedCallback2 インターフェイス](icordebugmanagedcallback2-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
