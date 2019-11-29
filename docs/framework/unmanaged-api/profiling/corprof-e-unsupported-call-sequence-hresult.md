---
title: CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT
ms.date: 03/30/2017
f1_keywords:
- CORPROF_E_UNSUPPORTED_CALL_SEQUENCE
helpviewer_keywords:
- CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT [.NET Framework profiling]
ms.assetid: f2fc441f-d62e-4f72-a011-354ea13c8c59
ms.openlocfilehash: 4d835f749a33d21a13be307e1524671e36496899
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74440829"
---
# <a name="corprof_e_unsupported_call_sequence-hresult"></a>CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT
CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT は .NET Framework バージョン2.0 で導入されました。 .NET Framework 4 は、次の2つのシナリオでこの HRESULT を返します。  
  
- ハイジャックプロファイラーが任意のタイミングでスレッドのレジスタコンテキストを強制的にリセットすると、スレッドは不整合な状態にある構造体にアクセスしようとします。  
  
- プロファイラーが、ガベージコレクションを禁止するコールバックメソッドからガベージコレクションをトリガーする情報メソッドを呼び出そうとしたとき。  
  
 これらの2つのシナリオについては、次のセクションで説明します。  
  
## <a name="hijacking-profilers"></a>プロファイラーのハイジャック  
 (このシナリオは、主にハイジャックプロファイラーの問題ですが、ハイジャックされていないプロファイラーでこの HRESULT が表示される場合もあります)。  
  
 このシナリオでは、ハイジャックプロファイラーは、スレッドがプロファイラーコードを入力したり、 [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)メソッドを使用して共通言語ランタイム (CLR) を再入力したりできるように、任意のタイミングでスレッドのレジスタコンテキストを強制的にリセットします。  
  
 プロファイリング API が CLR のデータ構造をポイントするために使用する Id の多く。 多くの `ICorProfilerInfo` 呼び出しでは、これらのデータ構造から情報を読み取って戻すだけです。 ただし、CLR では、実行時にこれらの構造内の項目が変更される可能性があり、ロックを使用することもあります。 プロファイラーがスレッドをハイジャックしたときに、CLR がロックを既に保持している (または取得しようとしている) とします。 スレッドが CLR に再入力し、さらに多くのロックを取得しようとした場合、または変更処理中の構造を検査する場合、これらの構造は不整合な状態になる可能性があります。 このような状況では、デッドロックとアクセス違反が簡単に発生します。  
  
 一般に、ハイジャックされていないプロファイラーが[ICorProfilerCallback](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)メソッド内でコードを実行し、有効なパラメーターを使用して `ICorProfilerInfo` メソッドを呼び出すと、デッドロックが発生したりアクセス違反が発生したりすることはありません。 たとえば、 [ICorProfilerCallback:: ClassLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-classloadfinished-method.md)メソッド内で実行されるプロファイラーコードは、 [ICorProfilerInfo2:: GetClassIDInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassidinfo2-method.md)メソッドを呼び出すことによって、クラスに関する情報を要求する場合があります。 このコードでは、情報が使用できないことを示すために CORPROF_E_DATAINCOMPLETE HRESULT が返される場合があります。ただし、デッドロックが発生したり、アクセス違反が発生したりすることはありません。 `ICorProfilerInfo` のこのクラス呼び出しは、`ICorProfilerCallback` メソッドから作成されるため、同期と呼ばれます。  
  
 ただし、`ICorProfilerCallback` メソッド内に含まれていないコードを実行するマネージスレッドは、非同期呼び出しを行うと見なされます。 .NET Framework バージョン1では、非同期呼び出しで発生する可能性があることを判断するのは困難でした。 この呼び出しは、デッドロック、クラッシュ、または無効な回答を与える可能性があります。 .NET Framework バージョン2.0 では、この問題を回避するための簡単なチェックがいくつか導入されました。 .NET Framework 2.0 では、unsafe `ICorProfilerInfo` 関数を非同期的に呼び出すと、CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT で失敗します。  
  
 一般に、非同期呼び出しは安全ではありません。 ただし、次のメソッドは安全であり、特に非同期呼び出しをサポートしています。  
  
- [GetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-geteventmask-method.md)  
  
- [SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)  
  
- [GetCurrentThreadID](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcurrentthreadid-method.md)  
  
- [GetThreadContext](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadcontext-method.md)  
  
- [GetThreadAppDomain](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getthreadappdomain-method.md)  
  
- [GetFunctionFromIP](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromip-method.md)  
  
- [GetFunctionInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctioninfo-method.md)  
  
- [GetFunctionInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md)  
  
- [GetCodeInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcodeinfo-method.md)  
  
- [GetCodeInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md)  
  
- [GetModuleInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmoduleinfo-method.md)  
  
- [GetClassIDInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassidinfo-method.md)  
  
- [GetClassIDInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassidinfo2-method.md)  
  
- [IsArrayClass](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-isarrayclass-method.md)  
  
- [SetFunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)  
  
- [DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)  
  
 詳細については、CLR プロファイル API のブログで[CORPROF_E_UNSUPPORTED_CALL_SEQUENCE した理由](https://go.microsoft.com/fwlink/?LinkId=169156)を参照してください。  
  
## <a name="triggering-garbage-collections"></a>ガベージコレクションのトリガー  
 このシナリオでは、ガベージコレクションを禁止するコールバックメソッド (たとえば、`ICorProfilerCallback` メソッドの1つ) 内で実行されているプロファイラーを使用します。 プロファイラーが、ガベージコレクションをトリガーする可能性のある情報メソッド (`ICorProfilerInfo` インターフェイスのメソッドなど) を呼び出そうとすると、情報メソッドが CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT で失敗します。  
  
 次の表は、ガベージコレクションを禁止するコールバックメソッドと、ガベージコレクションをトリガーする可能性のある情報メソッドを示しています。 プロファイラーが、一覧表示されているいずれかのコールバックメソッド内で実行され、一覧表示されている情報メソッドの1つを呼び出すと、その情報メソッドが CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT で失敗します。  
  
|ガベージコレクションを禁止するコールバックメソッド|ガベージコレクションをトリガーする情報メソッド|  
|------------------------------------------------------|------------------------------------------------------------|  
|[ThreadAssignedToOSThread](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-threadassignedtoosthread-method.md)<br /><br /> [ExceptionUnwindFunctionEnter](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfunctionenter-method.md)<br /><br /> [ExceptionUnwindFunctionLeave](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfunctionleave-method.md)<br /><br /> [ExceptionUnwindFinallyEnter](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfinallyenter-method.md)<br /><br /> [ExceptionUnwindFinallyLeave](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptionunwindfinallyleave-method.md)<br /><br /> [ExceptionCatcherEnter](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptioncatcherenter-method.md)<br /><br /> [RuntimeSuspendStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendstarted-method.md)<br /><br /> [RuntimeSuspendFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendfinished-method.md)<br /><br /> [RuntimeSuspendAborted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimesuspendaborted-method.md)<br /><br /> [RuntimeThreadSuspended](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadsuspended-method.md)<br /><br /> [RuntimeThreadResumed](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-runtimethreadresumed-method.md)<br /><br /> [MovedReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-movedreferences-method.md)<br /><br /> [ObjectReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectreferences-method.md)<br /><br /> [ObjectsAllocatedByClass](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectsallocatedbyclass-method.md)<br /><br /> [RootReferences2](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md)<br /><br /> [HandleCreated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-handlecreated-method.md)<br /><br /> [HandleDestroyed](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-handledestroyed-method.md)<br /><br /> [GarbageCollectionStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionstarted-method.md)<br /><br /> [GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md)|[GetILFunctionBodyAllocator](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbodyallocator-method.md)<br /><br /> [SetILFunctionBody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md)<br /><br /> [SetILInstrumentedCodeMap](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)<br /><br /> [ForceGC](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-forcegc-method.md)<br /><br /> [GetClassFromToken](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromtoken-method.md)<br /><br /> [GetClassFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassfromtokenandtypeargs-method.md)<br /><br /> [GetFunctionFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md)<br /><br /> [GetAppDomainInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getappdomaininfo-method.md)<br /><br /> [EnumModules](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enummodules-method.md)<br /><br /> [RequestProfilerDetach](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-requestprofilerdetach-method.md)<br /><br /> [GetAppDomainsContainingModule](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getappdomainscontainingmodule-method.md)|  
  
## <a name="see-also"></a>参照

- [ICorProfilerCallback インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ICorProfilerCallback2 インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-interface.md)
- [ICorProfilerCallback3 インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-interface.md)
- [ICorProfilerInfo インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
- [ICorProfilerInfo3 インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [プロファイル](../../../../docs/framework/unmanaged-api/profiling/index.md)
