---
title: ICorProfilerInfo インターフェイス
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo
helpviewer_keywords:
- ICorProfilerInfo interface [.NET Framework profiling]
ms.assetid: eb4e4ce0-06e7-4469-bbc4-edc2eb5da4b1
topic_type:
- apiref
ms.openlocfilehash: 0af990930e8c30307e9da3b586621ca8ddb95d0c
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74438754"
---
# <a name="icorprofilerinfo-interface"></a>ICorProfilerInfo インターフェイス
コードプロファイラーが共通言語ランタイム (CLR) と通信してイベントの監視および要求情報を制御するために使用するメソッドを提供します。  
  
> [!NOTE]
> `ICorProfilerInfo` インターフェイスの各メソッドは、成功または失敗を示す HRESULT を返します。 使用できるリターンコードの一覧については、「CorError. h」を参照してください。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[BeginInprocDebugging メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-begininprocdebugging-method.md)|インプロセスデバッグサポートを初期化します。 このメソッドは .NET Framework バージョン2.0 では廃止されています。|  
|[EndInprocDebugging メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-endinprocdebugging-method.md)|インプロセスデバッグセッションをシャットダウンします。 このメソッドは .NET Framework バージョン2.0 では廃止されています。|  
|[ForceGC メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-forcegc-method.md)|ランタイム内で強制的にガベージコレクションを実行します。|  
|[GetAppDomainInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getappdomaininfo-method.md)|指定されたアプリケーションドメインに関する情報を取得します。|  
|[GetAssemblyInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getassemblyinfo-method.md)|指定したアセンブリに関する情報を取得します。|  
|[GetClassFromObject メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromobject-method.md)|の `ClassID` を取得します。<br /><br /> オブジェクト (`ObjectID`を指定)。|  
|[GetClassFromToken メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromtoken-method.md)|メタデータトークンを指定して、クラスの ID を取得します。 このメソッドは .NET Framework バージョン2.0 では廃止されています。 代わりに[ICorProfilerInfo2:: GetClassFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassfromtokenandtypeargs-method.md)メソッドを使用してください。|  
|[GetClassIDInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassidinfo-method.md)|指定したクラスの親モジュールとメタデータトークンを取得します。|  
|[GetCodeInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcodeinfo-method.md)|指定した関数 ID に関連付けられているネイティブ コードの範囲を取得します。 このメソッドは、互換性のために残されています。 代わりに[ICorProfilerInfo2:: GetCodeInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md)メソッドを使用してください。|  
|[GetCurrentThreadID メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcurrentthreadid-method.md)|マネージスレッドの場合、現在のスレッドの ID を取得します。|  
|[GetEventMask メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-geteventmask-method.md)|プロファイラーが CLR からイベント通知を受信する現在のイベントカテゴリを取得します。|  
|[GetFunctionFromIP メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromip-method.md)|マネージコード命令ポインターを `FunctionID`にマップします。|  
|[GetFunctionFromToken メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromtoken-method.md)|関数の ID を取得します。 このメソッドは .NET Framework バージョン2.0 では廃止されています。 代わりに[ICorProfilerInfo2:: GetFunctionFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md)メソッドを使用してください。|  
|[GetFunctionInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctioninfo-method.md)|指定された関数の親クラスとメタデータトークンを取得します。|  
|[GetHandleFromThread メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-gethandlefromthread-method.md)|スレッドの ID を Win32 スレッドハンドルにマップします。|  
|[GetILFunctionBody メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbody-method.md)|Microsoft 中間言語 (MSIL) コード内のメソッドの本文へのポインターを、ヘッダーを開始位置として取得します。|  
|[GetILFunctionBodyAllocator メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbodyallocator-method.md)|MSIL コードでメソッドの本体を交換するために使用されるメモリを割り当てるメソッドを提供するインターフェイスを取得します。|  
|[GetILToNativeMapping メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md)|指定された関数に含まれるコードの MSIL オフセットからネイティブオフセットへのマップを取得します。|  
|[GetInprocInspectionInterface メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getinprocinspectioninterface-method.md)|は、のプロセスインターフェイスに対してクエリを実行できるオブジェクトを取得します。 このメソッドは .NET Framework バージョン2.0 では廃止されています。|  
|[GetInprocInspectionIThisThread メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getinprocinspectionithisthread-method.md)|のオブジェクトインターフェイスに対してクエリを実行できるオブジェクトを取得します。 このメソッドは .NET Framework バージョン2.0 では廃止されています。|  
|[GetModuleInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmoduleinfo-method.md)|モジュール ID を指定して、モジュールのファイル名とモジュールの親アセンブリの ID を取得します。|  
|[GetModuleMetaData メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md)|指定したモジュールにマップされるメタデータインターフェイスインスタンスを取得します。|  
|[GetObjectSize メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getobjectsize-method.md)|指定したオブジェクトのサイズを取得します。|  
|[GetThreadContext メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadcontext-method.md)|指定したスレッドに現在関連付けられているコンテキスト id を取得します。|  
|[GetThreadInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadinfo-method.md)|指定したスレッドの現在の Win32 スレッド id を取得します。|  
|[GetTokenAndMetadataFromFunction メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-gettokenandmetadatafromfunction-method.md)|メタデータトークンと、指定された関数のトークンに対して使用できるメタデータインターフェイスのインスタンスを取得します。|  
|[IsArrayClass メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-isarrayclass-method.md)|指定したクラスが配列クラスであるかどうかを判断します。|  
|[SetEnterLeaveFunctionHooks メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setenterleavefunctionhooks-method.md)|マネージ関数の "enter"、"leave"、および "tailcall" フックで呼び出されるプロファイラー実装関数を指定します。|  
|[SetEventMask メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)|プロファイラーが CLR からの通知の受信を希望するイベントの種類を指定する値を設定します。|  
|[SetFunctionIDMapper メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)|`FunctionID` 値を代替値に対応付けるために呼び出すプロファイラー実装関数を指定します。代替値は、プロファイラーの関数の開始フックと終了フックに渡されます。|  
|[SetFunctionReJIT メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionrejit-method.md)|実装されていません。 使わないでください。|  
|[SetILFunctionBody メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md)|指定したモジュール内の指定した関数の本体を置き換えます。|  
|[SetILInstrumentedCodeMap メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)|指定された関数の元の MSIL のオフセットが、関数のプロファイラーによって変更された MSIL の新しいオフセットにどのようにマップされるかを指定します。|  
  
## <a name="remarks"></a>コメント  
 プロファイラーは、CLR と通信してイベントの監視と要求情報を制御するために、`ICorProfilerInfo` インターフェイス内のメソッドを呼び出します。  
  
 `ICorProfilerInfo` インターフェイスのメソッドは、フリースレッドモデルを使用して CLR によって実装されます。 各メソッドが、成功または失敗を示す HRESULT を返します。 使用できるリターンコードの一覧については、「CorError. h」を参照してください。  
  
 CLR は、 [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)のプロファイラーの実装を介して、初期化中に各コードプロファイラーへの `ICorProfilerInfo` インターフェイスを渡します。 コードプロファイラーは、`ICorProfilerInfo` インターフェイスのメソッドを呼び出して、CLR の制御下で実行されているマネージコードに関する情報を取得できます。  
  
## <a name="requirements"></a>要件  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerInfo2 インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
