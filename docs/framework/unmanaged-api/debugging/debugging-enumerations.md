---
title: 列挙体のデバッグ
ms.date: 03/30/2017
helpviewer_keywords:
- debugging enumerations [.NET Framework]
- unmanaged enumerations [.NET Framework], debugging
- enumerations [.NET Framework debugging]
ms.assetid: 3af9f584-f1b4-4154-aeaa-8fce7c9f8b50
ms.openlocfilehash: c37b6ff42b428184d301d63b6dbbd9d80a72bf3f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179140"
---
# <a name="debugging-enumerations"></a>列挙体のデバッグ
このセクションでは、デバッグ API が使用するアンマネージ列挙体について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [CLR_DEBUGGING_PROCESS_FLAGS 列挙体](clr-debugging-process-flags-enumeration.md)  
 メソッドによって使用される値を提供[します](iclrdebugging-openvirtualprocess-method.md)。  
  
 [CLRDataEnumMemoryFlags 列挙型](clrdataenummemoryflags-enumeration.md)  
 メソッドに対する呼び出しに含めるメモリ領域[を示します](iclrdataenummemoryregions-enummemoryregions-method.md)。  
  
 [COR_PUB_ENUMPROCESS 列挙型](cor-pub-enumprocess-enumeration.md)  
 列挙するプロセスの型を識別します。  
  
 [CorDebugBlockingReason 列挙体](cordebugblockingreason-enumeration.md)  
 指定されたオブジェクト上でスレッドがブロックされる理由を指定します。  
  
 CorDebugChainReason  
 呼び出しチェーンが開始する理由を示します。  
  
 [CorDebugCodeInvokeKind 列挙体](cordebugcodeinvokekind-enumeration.md)  
 エクスポートされた関数がマネージド コードを呼び出す方法を示します。  
  
 [CorDebugCodeInvokePurpose 列挙体](cordebugcodeinvokepurpose-enumeration.md)  
 エクスポートされた関数がマネージド コードを呼び出す理由を示します。  
  
 CorDebugCreateProcessFlags  
 [メソッドの](icordebug-createprocess-method.md)呼び出しで使用できる追加のデバッグ オプションを提供します。  
  
 [CorDebugDebugEventKind 列挙体](cordebugdebugeventkind-enumeration.md)  
 [情報がデコード](icordebugprocess6-decodeevent-method.md)されるイベントの種類を示す、 DecodeEvent メソッドです。  
  
 [CorDebugDecodeEventFlagsWindows 列挙体](cordebugdecodeeventflagswindows-enumeration.md)  
 Windows プラットフォームのデバッグ イベントに関する追加情報を提供します。  
  
 CorDebugExceptionCallbackType  
 から行われるコールバックの[種類を示](icordebugmanagedcallback2-exception-method.md)します。  
  
 [CorDebugExceptionFlags 列挙型](cordebugexceptionflags-enumeration.md)  
 例外に関する追加情報を提供します。  
  
 CorDebugExceptionUnwindCallbackType  
 アンワインド フェーズ中にコールバックによって通知されるイベントを示します。  
  
 [CorDebugGCType 列挙型](cordebuggctype-enumeration.md)  
 ガベージ コレクターがワークステーションまたはサーバーのどちらで実行されているかを示します。  
  
 [CorDebugGenerationTypes 列挙型](cordebuggenerationtypes-enumeration.md)  
 マネージド ヒープ上のメモリ領域の生成を指定します。  
  
 CorDebugHandleType  
 ハンドル型を示します。  
  
 [CorDebugIlToNativeMappingTypes 列挙型](cordebugiltonativemappingtypes-enumeration.md)  
 ネイティブ命令の特定の範囲が特別なコード領域に対応するかどうかを示します。  
  
 CorDebugIntercept  
 ステップ インできるコードの型を示します。  
  
 [CorDebugInterfaceVersion 列挙型](cordebuginterfaceversion-enumeration.md)  
 .NET Framework のバージョン、またはインターフェイスが導入された .NET Framework のバージョンのいずれかを指定します。  
  
 CorDebugInternalFrameType  
 スタック フレームの型を示します。  
  
 [CorDebugJITCompilerFlags 列挙型](cordebugjitcompilerflags-enumeration.md)  
 マネージド Just-In-Time (JIT) コンパイラの動作に影響を与える値が含まれます。  
  
 [CorDebugJITCompilerFlagsDeprecated 列挙型](cordebugjitcompilerflagsdeprecated-enumeration.md)  
 互換性のために残されています。 代わりに`CORDEBUG_JIT_DEFAULT`、列挙体のメンバー[を](cordebugjitcompilerflags-enumeration.md)使用します。  
  
 CorDebugMappingResult  
 命令ポインター (IP) の値が得られた方法の詳細を提供します。  
  
 [CorDebugMDAFlags 列挙型](cordebugmdaflags-enumeration.md)  
 マネージド デバッグ アシスタント (MDA) が生成されるスレッドのステータスを指定します。  
  
 [CorDebugNGenPolicy 列挙型](cordebugngenpolicy-enumeration.md)  
 デバッガーがネイティブ イメージ キャッシュからネイティブ (NGen) イメージを読み込むかどうかを指定する値を提供します。  
  
 [CorDebugPlatform 列挙型](cordebugplatform-enumeration.md)  
 メソッドによって使用されるターゲット プラットフォームの値[を提供します](icordebugdatatarget-getplatform-method.md)。  
  
 [CorDebugRecordFormat 列挙体](cordebugrecordformat-enumeration.md)  
 ネイティブ例外デバッグ イベントに関する情報を格納するバイト配列内のデータの形式を示します。  
  
 CorDebugRegister  
 指定されたプロセッサ アーキテクチャに関連付けられたレジスタを指定します。  
  
 [CorDebugSetContextFlag 列挙体](cordebugsetcontextflag-enumeration.md)  
 スタック上のアクティブ (またはリーフ) フレーム上からのコンテキストなのか、別のフレームからのアンワインドにより計算されたコンテキストなのかを示します。  
  
 [CorDebugStateChange 列挙体](cordebugstatechange-enumeration.md)  
 プロセスへの変更に基づいて破棄が必要となった、キャッシュされたデータの量を示します。  
  
 CorDebugStepReason  
 個々のステップの結果を示します。  
  
 CorDebugThreadState  
 デバッグのスレッドの状態を指定します。  
  
 \>マップされていない停止  
 ステッパによるコード実行の停止をトリガーする可能性のあるマップ解除したコードの型を指定します。  
  
 CorDebugUserState  
 スレッドのユーザーの状態を示します。  
  
 [CorGCReferenceType 列挙型](corgcreferencetype-enumeration.md)  
 ガベージ コレクトされる必要のあるオブジェクトのソースを識別します。  
  
 [ILCodeKind 列挙型](ilcodekind-enumeration.md)  
 デバッガーがローカル変数またはプロファイラー ReJIT インストルメンテーションに追加されたコードにアクセスできるかどうかを指定する値を提供します。  
  
 [LoggingLevelEnum 列挙型](logginglevelenum-enumeration.md)  
 マネージド スレッドがイベントを記録する際にイベント ログに書き込まれる説明メッセージの重大度レベルを示します。  
  
 [LogSwitchCallReason 列挙型](logswitchcallreason-enumeration.md)  
 デバッグとトレースの切り替えで実行された操作を示します。  
  
 [VariableLocationType 列挙型](variablelocationtype-enumeration.md)  
 変数のネイティブな場所の型を示します。  
  
 [WriteableMetadataUpdateMode 列挙型](writeablemetadataupdatemode-enumeration.md)  
 メモリ内のメタデータ更新をデバッガーに対して可視にするかどうかを指定する値を提供します。

 [列挙型](clrdatasourcetype-enumeration.md)CLRDATA_IL_ADDRESS_MAP構造体で使用される値を提供します。

## <a name="related-sections"></a>関連項目  
 [デバッグ コクラス](debugging-coclasses.md)  
  
 [デバッグ インターフェイス](debugging-interfaces.md)  
  
 [デバッグ グローバル静的関数](debugging-global-static-functions.md)  
  
 [デバッグ構造体](debugging-structures.md)
