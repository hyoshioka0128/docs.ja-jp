---
title: グローバル静的関数のプロファイル
ms.date: 03/30/2017
helpviewer_keywords:
- global static functions [.NET Framework profiling]
- profiling global static functions [.NET Framework]
- unmanaged global static functions [.NET Framework], profiling
ms.assetid: 08a13a57-dc49-488d-b937-31e3051fda97
ms.openlocfilehash: d1d9b0a4c61ce7c3f8f9792046fb4bddf0fdfa05
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74447438"
---
# <a name="profiling-global-static-functions"></a>グローバル静的関数のプロファイル
このセクションでは、プロファイリング API が使用するアンマネージ API 関数について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
## <a name="net-framework-version-1-profiling-functions"></a>.NET Framework version 1 プロファイリング関数  
 [FunctionEnter 関数](../../../../docs/framework/unmanaged-api/profiling/functionenter-function.md)  
 コントロールが関数に渡されていることをプロファイラーに通知します。 .NET Framework 2.0 では非推奨となりました。  
  
 [FunctionLeave 関数](../../../../docs/framework/unmanaged-api/profiling/functionleave-function.md)  
 関数が呼び出し元に戻りようとしていることをプロファイラーに通知します。 .NET Framework 2.0 では非推奨となりました。  
  
 [FunctionTailcall 関数](../../../../docs/framework/unmanaged-api/profiling/functiontailcall-function.md)  
 現在実行中の関数が別の関数の末尾呼び出しを実行しようとしていることをプロファイラーに通知します。 .NET Framework 2.0 では非推奨となりました。  
  
## <a name="net-framework-version-2-profiling-functions"></a>.NET Framework version 2 プロファイリング関数  
 [FunctionIDMapper 関数](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md)  
 関数の特定の識別子が、その関数の[FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)、 [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)、および[FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)コールバックで使用される代替 ID に再マップされる可能性があることをプロファイラーに通知します。 また、プロファイラーが、その関数のコールバックを受信するかどうかを示すこともできます。  
  
 [FunctionEnter2 関数](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)  
 コントロールが関数に渡されていることをプロファイラーに通知し、スタックフレームと関数の引数に関する情報を提供します。 .NET Framework 4 では非推奨となりました。  
  
 [FunctionLeave2 関数](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)  
 関数が呼び出し元に戻り、スタックフレームおよび関数の戻り値に関する情報を提供することをプロファイラーに通知します。 .NET Framework 4 では非推奨となりました。  
  
 [FunctionTailcall2 関数](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)  
 現在実行中の関数が別の関数の末尾呼び出しを実行しようとしていることをプロファイラーに通知し、スタックフレームに関する情報を提供します。 .NET Framework 4 では非推奨となりました。  
  
 [StackSnapshotCallback 関数](../../../../docs/framework/unmanaged-api/profiling/stacksnapshotcallback-function.md)  
 [ICorProfilerInfo2::D ostacksnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)メソッドによって開始されるスタックウォーク中に、各マネージフレームおよびスタック上のアンマネージフレームの各実行に関する情報をプロファイラーに提供します。  
  
## <a name="net-framework-version-4-profiling-functions"></a>.NET Framework version 4 プロファイリング関数  
 [FunctionIDMapper2 関数](../../../../docs/framework/unmanaged-api/profiling/functionidmapper2-function.md)  
 指定された関数の識別子が、その関数の[FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)、 [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)、 [FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)、または[FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)、 [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)、および[FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)コールバックで使用される代替 ID に再マップされる可能性があることをプロファイラーに通知します。 また、プロファイラーは、その関数のコールバックを受信するかどうかを示すこともできます。  
  
 `FunctionIDMapper2` は、`clientData` パラメーターを使用して[Functionidmapper](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md)関数を拡張します。これは、プロファイラーがランタイムを明確に区別するために使用する可能性があります。  
  
 [FunctionEnter3 関数](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)  
 コントロールが関数に渡されていることをプロファイラーに通知します。  
  
 [FunctionEnter3WithInfo 関数](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)  
 コントロールが関数に渡されていることをプロファイラーに通知し、スタックフレームと関数の引数を取得するために[ICorProfilerInfo3:: GetFunctionEnter3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionenter3info-method.md)に渡すことができるハンドルを提供します。  
  
 [FunctionLeave3 関数](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)  
 関数から制御が返されていることをプロファイラーに通知します。  
  
 [FunctionLeave3WithInfo 関数](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)  
 関数から制御が返されていることをプロファイラーに通知し、スタックフレームと戻り値を取得するために[ICorProfilerInfo3:: GetFunctionLeave3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md)に渡すことができるハンドルを提供します。  
  
 [FunctionTailcall3 関数](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)  
 現在実行中の関数が別の関数の末尾呼び出しを実行しようとしていることをプロファイラーに通知します。  
  
 [FunctionTailcall3WithInfo 関数](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)  
 現在実行中の関数が別の関数の末尾呼び出しを実行しようとしていることをプロファイラーに通知し、スタックフレームを取得するために[ICorProfilerInfo3:: GetFunctionTailcall3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md)に渡すことができるハンドルを提供します。  
  
## <a name="related-sections"></a>関連項目  
 [プロファイルの概要](../../../../docs/framework/unmanaged-api/profiling/profiling-overview.md)  
  
 [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
  
 [列挙型のプロファイリング](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)  
  
 [構造体のプロファイリング](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)
