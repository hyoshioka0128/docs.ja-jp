---
title: ICorProfilerCallback3::ProfilerDetachSucceeded メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback3.ProfilerDetachSucceeded Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback3::ProfilerDetachSucceeded
helpviewer_keywords:
- ProfilerDetachSucceeded method [.NET Framework profiling]
- ICorProfilerCallback3::ProfilerDetachSucceeded method [.NET Framework profiling]
ms.assetid: 05164966-16ce-4cc9-a530-43a640c00711
topic_type:
- apiref
ms.openlocfilehash: 93406dddf7babd8cf61032666737b993c2f721f4
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499598"
---
# <a name="icorprofilercallback3profilerdetachsucceeded-method"></a>ICorProfilerCallback3::ProfilerDetachSucceeded メソッド
共通言語ランタイム (CLR: Common Language Runtime) がプロファイラー DLL をアンロードしようとしていることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ProfilerDetachSucceeded();  
```  
  
## <a name="return-value"></a>戻り値  
 このコールバックからの戻り値は無視されます。  
  
## <a name="remarks"></a>解説  
 `ProfilerDetachSucceeded` コールバックは、すべてのスレッドでプロファイラーのコードが終了した後に発行されます。 このメソッドが呼び出された場合、プロファイラーは、そのデストラクターに適さない最後の段階のタスク (その UI またはログ コンポーネントの通知など) を実行する必要があります。 ただし、プロファイラーは、このコールバック中に CLR によって提供されるインターフェイス ( [ICorProfilerInfo](icorprofilerinfo-interface.md)やインターフェイスなど) で関数を呼び出すことはできません `IMetaData*` 。  
  
 CLR は Windows アプリケーション イベント ログに、デタッチ操作が成功したことを示すエントリを作成します。  
  
 プロファイラーがこのコールバックから戻ると、CLR はプロファイラー オブジェクトを解放し、プロファイラー DLL をアンロードします。 したがって、プロファイラーは、コールバックから戻った後にプロファイラー DLL 内での実行を発生させるアクションを実行することはできません。 たとえば、プロファイラーは、スレッドを作成することも、タイマー コールバックを登録することもできません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ インターフェイス](../metadata/metadata-interfaces.md)
- [ICorProfilerInfo3 インターフェイス](icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
