---
title: ICorProfilerInfo2 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2
helpviewer_keywords:
- ICorProfilerInfo2 interface [.NET Framework profiling]
ms.assetid: 91bd49b6-4d12-494f-a8f1-2f251e8c65e3
topic_type:
- apiref
ms.openlocfilehash: fdac9eedb0ae442d6dd2646859cab13398020a87
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74449775"
---
# <a name="icorprofilerinfo2-interface"></a>ICorProfilerInfo2 インターフェイス
コードプロファイラーが共通言語ランタイム (CLR) と通信してイベント監視と要求情報を制御するために使用するメソッドを提供します。 `ICorProfilerInfo2` インターフェイスは、 [ICorProfilerInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)インターフェイスの拡張機能です。 つまり、.NET Framework バージョン2.0 以降のバージョンでサポートされている新しいメソッドが用意されています。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[DoStackSnapshot メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)|マネージ呼び出しフレームをプロファイラーに報告するために、指定したスレッドのスタックを走査します。|  
|[EnumModuleFrozenObjects メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-enummodulefrozenobjects-method.md)|指定したモジュール内の固定されたオブジェクトを反復処理できる列挙子を取得します。|  
|[GetAppDomainStaticAddress メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getappdomainstaticaddress-method.md)|指定したアプリケーションドメインのスコープ内にある、指定したアプリケーションドメインの静的フィールドのアドレスを取得します。|  
|[GetArrayObjectInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getarrayobjectinfo-method.md)|配列オブジェクトに関する詳細情報を取得します。|  
|[GetBoxClassLayout メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getboxclasslayout-method.md)|ボックス化された指定された値型のクラスレイアウトに関する情報を取得します。|  
|[GetClassFromTokenAndTypeArgs メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassfromtokenandtypeargs-method.md)|指定されたメタデータトークンと任意の型引数の `ClassID` 値を使用して、型の `ClassID` を取得します。|  
|[GetClassIDInfo2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassidinfo2-method.md)|指定されたジェネリッククラスの親モジュール、クラスのメタデータトークン、その親クラスの `ClassID`、およびクラスの型引数 (存在する場合) の `ClassID` を取得します。|  
|[GetClassLayout メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclasslayout-method.md)|指定したクラスで定義されるフィールドのメモリ内レイアウトに関する情報を取得します。 つまり、このメソッドはクラスのフィールドのオフセットを取得します。|  
|[GetCodeInfo2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md)|指定した `FunctionID` に関連付けられているネイティブ コードの範囲を取得します。|  
|[GetContextStaticAddress メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcontextstaticaddress-method.md)|指定されたコンテキストのスコープ内にある、指定されたコンテキスト静的フィールドのアドレスを取得します。|  
|[GetFunctionFromTokenAndTypeArgs メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md)|指定されたメタデータトークン、格納クラス、および任意の型引数の `ClassID` 値を使用して、関数の `FunctionID` を取得します。|  
|[GetFunctionInfo2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctioninfo2-method.md)|関数の親クラス、メタデータ トークン、および型引数が存在する場合はそれぞれの `ClassID` を取得します。|  
|[GetGenerationBounds メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getgenerationbounds-method.md)|ガベージコレクトされたヒープのジェネレーションを構成するメモリ領域 (ヒープのセグメント) を取得します。|  
|[GetNotifiedExceptionClauseInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getnotifiedexceptionclauseinfo-method.md)|実行される、または実行される直前の例外句 (`catch`/`finally`/`filter`) のネイティブアドレスとフレーム情報を取得します。|  
|[GetObjectGeneration メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getobjectgeneration-method.md)|指定されたオブジェクトを格納しているヒープのセグメントを取得します。|  
|[GetRVAStaticAddress メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getrvastaticaddress-method.md)|指定された相対仮想アドレス (RVA) の静的フィールドのアドレスを取得します。|  
|[GetStaticFieldInfo メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getstaticfieldinfo-method.md)|指定したフィールドが静的であるスコープを取得します。|  
|[GetStringLayout メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getstringlayout-method.md)|文字列オブジェクトのレイアウトに関する情報を取得します。|  
|[GetThreadAppDomain メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getthreadappdomain-method.md)|指定したスレッドが現在コードを実行しているアプリケーションドメインの ID を取得します。|  
|[GetThreadStaticAddress メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getthreadstaticaddress-method.md)|指定したスレッドのスコープ内にある、指定したスレッド静的フィールドのアドレスを取得します。|  
|[SetEnterLeaveFunctionHooks2 メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)|マネージ関数の "enter"、"leave"、および "tailcall" フックで呼び出されるプロファイラー実装関数を指定します。|  
  
## <a name="remarks"></a>コメント  
 プロファイラーは、CLR と通信してイベントの監視と要求情報を制御するために、`ICorProfilerInfo2` インターフェイス内のメソッドを呼び出します。  
  
 `ICorProfilerInfo2` インターフェイスのメソッドは、フリースレッドモデルを使用して CLR によって実装されます。 各メソッドが、成功または失敗を示す HRESULT を返します。 返される可能性があるリターン コードの一覧については、CorError.h ファイルを参照してください。  
  
 CLR は、 [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)のプロファイラーの実装を使用して、初期化中に各コードプロファイラーに `ICorProfilerInfo2` インターフェイスを渡します。 コードプロファイラーは、`ICorProfilerInfo2` インターフェイスのメソッドを呼び出して、CLR の制御下で実行されているマネージコードに関する情報を取得できます。  
  
## <a name="requirements"></a>要件  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>参照

- [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerInfo インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
