---
title: ICorProfilerCallback::JITCachedFunctionSearchFinished メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCachedFunctionSearchFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCachedFunctionSearchFinished
helpviewer_keywords:
- JITCachedFunctionSearchFinished method [.NET Framework profiling]
- ICorProfilerCallback::JITCachedFunctionSearchFinished method [.NET Framework profiling]
ms.assetid: 3c325c82-cddd-4b00-b3da-e450c36abf62
topic_type:
- apiref
ms.openlocfilehash: 6efc9d407bb95f75a79252b2dfad85b396d2164a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500079"
---
# <a name="icorprofilercallbackjitcachedfunctionsearchfinished-method"></a>ICorProfilerCallback::JITCachedFunctionSearchFinished メソッド
以前にネイティブイメージジェネレーター (Ngen.exe) を使用してコンパイルされた関数の検索が終了したことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT JITCachedFunctionSearchFinished(  
    [in] FunctionID        functionId,  
    [in] COR_PRF_JIT_CACHE result);  
```  
  
## <a name="parameters"></a>パラメーター

- `functionId`

  \[in] 検索が実行された関数の ID。

- `result`

  \[in] 検索の結果を示す[COR_PRF_JIT_CACHE](cor-prf-jit-cache-enumeration.md)列挙体の値。

## <a name="remarks"></a>解説  
 .NET Framework バージョン2.0 では、通常の NGen イメージのすべての関数に対して[ICorProfilerCallback:: JITCachedFunctionSearchStarted](icorprofilercallback-jitcachedfunctionsearchstarted-method.md)と `JITCachedFunctionSearchFinished` コールバックは行われません。 プロファイラー用に最適化された NGen イメージのみが、イメージ内のすべての関数のコールバックを生成します。 ただし、オーバーヘッドが増加するため、プロファイラーは、これらのコールバックを使用して just-in-time (JIT) コンパイルを強制的に実行する場合にのみ、プロファイラーで最適化された NGen イメージを要求する必要があります。 それ以外の場合、プロファイラーは関数情報を収集するためにレイジー戦略を使用する必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
