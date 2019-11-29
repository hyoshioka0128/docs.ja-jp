---
title: ICorProfilerInfo3 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3
helpviewer_keywords:
- ICorProfilerInfo3 interface [.NET Framework profiling]
ms.assetid: 044a262f-0fa7-485d-b0c1-64cdc359c654
topic_type:
- apiref
ms.openlocfilehash: c42b0df90dc690997bbc5414e977d6830dc5f3b8
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74449631"
---
# <a name="icorprofilerinfo3-interface"></a>ICorProfilerInfo3 インターフェイス
コード プロファイラーが共通言語ランタイム (CLR: Common Language Runtime) とやり取りして、イベント監視を制御したり、情報を要求したりするために使用する各種メソッドを提供します。 `ICorProfilerInfo3` インターフェイスは、 [ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)インターフェイスの拡張機能です。 .NET Framework 4 以降のバージョンでサポートされている新しいメソッドが用意されています。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumJITedFunctions メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enumjitedfunctions-method.md)|以前に JIT でコンパイルされたすべての関数に対する列挙子を返します。|  
|[EnumModules メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enummodules-method.md)|アプリケーションに読み込まれるマネージド モジュールのコレクションを順番に反復処理するメソッドを提供する列挙子を返します。|  
|[GetAppDomainsContainingModule メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getappdomainscontainingmodule-method.md)|指定したモジュールが読み込まれているアプリケーション ドメインの識別子を取得します。|  
|[GetFunctionEnter3Info メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionenter3info-method.md)|[FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)関数によってプロファイラーに報告される関数のスタックフレームと引数の情報を提供します。`FunctionEnter3WithInfo` コールバック中にのみ呼び出すことができます。|  
|[GetFunctionLeave3Info メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md)|[FunctionLeave3WithInfo function](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)関数によってプロファイラーに報告される関数のスタックフレームと戻り値を提供します。`FunctionLeave3WithInfo` コールバック中にのみ呼び出すことができます。|  
|[GetFunctionTailcall3Info メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md)|[FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)関数によってプロファイラーに報告される関数のスタックフレームを提供します。`FunctionTailcall3WithInfo` コールバック中にのみ呼び出すことができます。|  
|[GetModuleInfo2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getmoduleinfo2-method.md)|モジュール ID を指定して、モジュールのファイル名、モジュールの親アセンブリの ID、およびモジュールのプロパティを示すビットマスクを返します。|  
|[GetRuntimeInformation メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getruntimeinformation-method.md)|プロファイリングされているランタイムに関するバージョン情報を提供します。|  
|[GetStringLayout2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getstringlayout2-method.md)|文字列オブジェクトのレイアウトに関する情報を取得します。|  
|[GetThreadStaticAddress2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getthreadstaticaddress2-method.md)|指定したスレッドおよびアプリケーション ドメインのスコープ内にある、指定したスレッド内静的フィールドのアドレスを取得します。|  
|[RequestProfilerDetach メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-requestprofilerdetach-method.md)|プロファイラーをデタッチするようにランタイムに指示します。|  
|[SetEnterLeaveFunctionHooks3 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3-method.md)|[FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)、 [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)、および[FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)の各関数で呼び出されるプロファイラー実装関数を指定します。|  
|[SetEnterLeaveFunctionHooks3WithInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)|マネージ関数の[FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)、 [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)、および[FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)フックで呼び出されるプロファイラー実装関数を指定します。|  
|[SetFunctionIDMapper2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setfunctionidmapper2-method.md)|`FunctionID` 値を代替値に対応付けるために呼び出すプロファイラー実装関数を指定します。代替値は、プロファイラーの関数の開始フックと終了フックに渡されます。 このメソッドは、 [ICorProfilerInfo:: SetFunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)を、プロファイラーがランタイム間を明確に区別するために使用するパラメーターを使用して拡張します。|  
  
## <a name="remarks"></a>コメント  
 CLR は、`ICorProfilerInfo3` インターフェイスのメソッドを、フリー スレッド モデルを使用して実装します。 各メソッドが、成功または失敗を示す HRESULT を返します。 返される可能性があるリターン コードの一覧については、CorError.h ファイルを参照してください。  
  
 CLR は、 [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)メソッドまたは[ICorProfilerCallback3:: initializeforattach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md)メソッドのプロファイラーの実装を使用して、初期化中に各コードプロファイラーに `ICorProfilerInfo3` インターフェイスを渡します。 その後、コード プロファイラーは `ICorProfilerInfo3` メソッドを呼び出して、CLR の制御下で実行中のマネージド コードに関する情報を取得できます。  
  
## <a name="requirements"></a>要件  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerInfo インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
