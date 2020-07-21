---
title: ICorProfilerCallback4::ReJITError メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.ReJITError
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::ReJITError
helpviewer_keywords:
- ReJITError method, ICorProfilerCallback4 interface [.NET Framework profiling]
- ICorProfilerCallback4::ReJITError method [.NET Framework profiling]
ms.assetid: d7888aa9-dfaa-420f-9f99-e06ab35ca482
topic_type:
- apiref
ms.openlocfilehash: 488069f3ea16352cb7bb5e81b9a726637a7a65f8
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499364"
---
# <a name="icorprofilercallback4rejiterror-method"></a>ICorProfilerCallback4::ReJITError メソッド
Just-in-time (JIT) コンパイラが再コンパイルプロセスでエラーを検出したことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ReJITError(  
    [in] ModuleID    moduleId,  
    [in] mdMethodDef methodId,  
    [in] FunctionID  functionId,  
    [in] HRESULT     hrStatus);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleID`  
 から再 `ModuleID` コンパイルの試行が失敗した。  
  
 `methodId`  
 から再 `MethodDef` コンパイルの試行が失敗したメソッドの。  
  
 `functionId`  
 から再コンパイルまたは再コンパイルのマークが付けられている関数インスタンス。 この値は、インスタンス化ごとではなく、メソッドごとにエラーが発生した場合に発生する可能性があり `NULL` ます (たとえば、プロファイラーが、再コンパイルするメソッドに対して無効なメタデータトークンを指定した場合など)。  
  
 `hrStatus`  
 からエラーの性質を示す HRESULT。 値の一覧については、「Status HRESULT」セクションを参照してください。  
  
## <a name="return-value"></a>戻り値  
 このコールバックからの戻り値は無視されます。  
  
## <a name="status-hresults"></a>状態 HRESULT  
  
|状態配列 HRESULT|説明|  
|--------------------------|-----------------|  
|E_INVALIDARG|`moduleID`または `methodDef` トークンが `NULL` です。|  
|CORPROF_E_DATAINCOMPLETE|モジュールが完全に読み込まれていないか、またはアンロード中です。|  
|CORPROF_E_MODULE_IS_DYNAMIC|指定されたモジュールは (などによって) 動的に生成された `Reflection.Emit` ため、このメソッドではサポートされません。|  
|CORPROF_E_FUNCTION_IS_COLLECTIBLE|メソッドは、収集可能なアセンブリにインスタンス化されるため、再コンパイルできません。 非リフレクションコンテキスト (たとえば、) で定義されている型と関数は、 `List<MyCollectibleStruct>` 収集可能なアセンブリにインスタンス化できます。|  
|E_OUTOFMEMORY|CLR は、指定されたメソッドに JIT 再コンパイルのマークを付けようとしている間にメモリ不足になりました。|  
|その他|オペレーティング システムは、CLR 制御範囲外のエラーを返しました。 たとえば、メモリページのアクセス保護を変更するシステムコールが失敗した場合、オペレーティングシステムエラーが表示されます。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [ICorProfilerCallback4 インターフェイス](icorprofilercallback4-interface.md)
