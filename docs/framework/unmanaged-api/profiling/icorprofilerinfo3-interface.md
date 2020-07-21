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
ms.openlocfilehash: 0a474719935ba763cbd15dc6e18fe5ba99c14ebc
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496309"
---
# <a name="icorprofilerinfo3-interface"></a>ICorProfilerInfo3 インターフェイス
コード プロファイラーが共通言語ランタイム (CLR: Common Language Runtime) とやり取りして、イベント監視を制御したり、情報を要求したりするために使用する各種メソッドを提供します。 インターフェイスは、 `ICorProfilerInfo3` [ICorProfilerInfo2](icorprofilerinfo2-interface.md)インターフェイスの拡張機能です。 .NET Framework 4 以降のバージョンでサポートされている新しいメソッドが用意されています。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumJITedFunctions メソッド](icorprofilerinfo3-enumjitedfunctions-method.md)|以前に JIT でコンパイルされたすべての関数に対する列挙子を返します。|  
|[EnumModules メソッド](icorprofilerinfo3-enummodules-method.md)|アプリケーションに読み込まれるマネージド モジュールのコレクションを順番に反復処理するメソッドを提供する列挙子を返します。|  
|[GetAppDomainsContainingModule メソッド](icorprofilerinfo3-getappdomainscontainingmodule-method.md)|指定したモジュールが読み込まれているアプリケーション ドメインの識別子を取得します。|  
|[GetFunctionEnter3Info メソッド](icorprofilerinfo3-getfunctionenter3info-method.md)|[FunctionEnter3WithInfo](functionenter3withinfo-function.md)関数によってプロファイラーに報告される関数のスタックフレームと引数の情報を提供します。は、コールバック中にのみ呼び出すことができ `FunctionEnter3WithInfo` ます。|  
|[GetFunctionLeave3Info メソッド](icorprofilerinfo3-getfunctionleave3info-method.md)|[FunctionLeave3WithInfo function](functionleave3withinfo-function.md)関数によってプロファイラーに報告される関数のスタックフレームと戻り値を提供します。は、コールバック中にのみ呼び出すことができ `FunctionLeave3WithInfo` ます。|  
|[GetFunctionTailcall3Info メソッド](icorprofilerinfo3-getfunctiontailcall3info-method.md)|[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)関数によってプロファイラーに報告される関数のスタックフレームを提供します。は、コールバック中にのみ呼び出すことができ `FunctionTailcall3WithInfo` ます。|  
|[GetModuleInfo2 メソッド](icorprofilerinfo3-getmoduleinfo2-method.md)|モジュール ID を指定して、モジュールのファイル名、モジュールの親アセンブリの ID、およびモジュールのプロパティを示すビットマスクを返します。|  
|[GetRuntimeInformation メソッド](icorprofilerinfo3-getruntimeinformation-method.md)|プロファイリングされているランタイムに関するバージョン情報を提供します。|  
|[GetStringLayout2 メソッド](icorprofilerinfo3-getstringlayout2-method.md)|文字列オブジェクトのレイアウトに関する情報を取得します。|  
|[GetThreadStaticAddress2 メソッド](icorprofilerinfo3-getthreadstaticaddress2-method.md)|指定したスレッドおよびアプリケーション ドメインのスコープ内にある、指定したスレッド内静的フィールドのアドレスを取得します。|  
|[RequestProfilerDetach メソッド](icorprofilerinfo3-requestprofilerdetach-method.md)|プロファイラーをデタッチするようにランタイムに指示します。|  
|[SetEnterLeaveFunctionHooks3 メソッド](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)|[FunctionEnter3](functionenter3-function.md)、 [FunctionLeave3](functionleave3-function.md)、および[FunctionTailcall3](functiontailcall3-function.md)の各関数で呼び出されるプロファイラー実装関数を指定します。|  
|[SetEnterLeaveFunctionHooks3WithInfo メソッド](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)|マネージ関数の[FunctionEnter3WithInfo](functionenter3withinfo-function.md)、 [FunctionLeave3WithInfo](functionleave3withinfo-function.md)、および[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)フックで呼び出されるプロファイラー実装関数を指定します。|  
|[SetFunctionIDMapper2 メソッド](icorprofilerinfo3-setfunctionidmapper2-method.md)|`FunctionID` 値を代替値に対応付けるために呼び出すプロファイラー実装関数を指定します。代替値は、プロファイラーの関数の開始フックと終了フックに渡されます。 このメソッドは、 [ICorProfilerInfo:: SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md)を、プロファイラーがランタイム間を明確に区別するために使用するパラメーターを使用して拡張します。|  
  
## <a name="remarks"></a>解説  
 CLR は、`ICorProfilerInfo3` インターフェイスのメソッドを、フリー スレッド モデルを使用して実装します。 各メソッドが、成功または失敗を示す HRESULT を返します。 返される可能性があるリターン コードの一覧については、CorError.h ファイルを参照してください。  
  
 CLR は、 `ICorProfilerInfo3` [ICorProfilerCallback:: Initialize](icorprofilercallback-initialize-method.md)メソッドまたは[ICorProfilerCallback3:: initializeforattach](icorprofilercallback3-initializeforattach-method.md)メソッドのプロファイラーの実装を使用して、初期化中に各コードプロファイラーにインターフェイスを渡します。 その後、コード プロファイラーは `ICorProfilerInfo3` メソッドを呼び出して、CLR の制御下で実行中のマネージド コードに関する情報を取得できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
