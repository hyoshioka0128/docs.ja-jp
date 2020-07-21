---
title: ICorProfilerCallback::JITCachedFunctionSearchStarted メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCachedFunctionSearchStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCachedFunctionSearchStarted
helpviewer_keywords:
- JITCachedFunctionSearchStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCachedFunctionSearchStarted method [.NET Framework profiling]
ms.assetid: 5cba642c-0d80-48ee-889d-198c5044d821
topic_type:
- apiref
ms.openlocfilehash: d8f4a04abea0bd5eb9bf38629a8fcaf76479bcc9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500060"
---
# <a name="icorprofilercallbackjitcachedfunctionsearchstarted-method"></a>ICorProfilerCallback::JITCachedFunctionSearchStarted メソッド
以前にネイティブイメージジェネレーター (Ngen.exe) を使用してコンパイルされた関数に対して検索が開始されたことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT JITCachedFunctionSearchStarted(  
    [in]  FunctionID functionId,  
    [out] BOOL *pbUseCachedFunction);  
```  
  
## <a name="parameters"></a>パラメーター

- `functionId`

  \[in] 検索を実行する関数の ID。

- `pbUseCachedFunction`

  \[out] `true` (使用可能な場合) キャッシュされたバージョンの関数を実行エンジンが使用する必要がある場合は。それ以外の場合は `false` 。 値がの場合、 `false` 実行エンジンは、jit コンパイルされていないバージョンを使用するのではなく、関数を jit コンパイルします。

## <a name="remarks"></a>解説  
 .NET Framework バージョン2.0 では、 `JITCachedFunctionSearchStarted` 通常の NGen イメージのすべての関数に対して、および[ICorProfilerCallback:: JITCachedFunctionSearchFinished メソッド](icorprofilercallback-jitcachedfunctionsearchfinished-method.md)のコールバックは行われません。 プロファイル用に最適化された NGen イメージのみが、イメージ内のすべての関数のコールバックを生成します。 ただし、オーバーヘッドが増加するため、プロファイラーは、これらのコールバックを使用して just-in-time (JIT) コンパイルを強制的に実行する場合にのみ、プロファイラーで最適化された NGen イメージを要求する必要があります。 それ以外の場合、プロファイラーは関数情報を収集するためにレイジー戦略を使用する必要があります。  
  
 プロファイラーは、プロファイルされたアプリケーションの複数のスレッドが同時に同じメソッドを呼び出す場合をサポートする必要があります。 たとえば、スレッド A がを呼び出し、 `JITCachedFunctionSearchStarted` プロファイラーは、 *PBUSECACHEDFUNCTION*を FALSE に設定して JIT コンパイルを強制することで応答します。 次に、スレッド A は[ICorProfilerCallback:: JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md)と[ICorProfilerCallback:: JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md)を呼び出します。  
  
 ここで、スレッド B `JITCachedFunctionSearchStarted` は同じ関数を呼び出します。 プロファイラーは、関数を JIT コンパイルすることを意図していましたが、プロファイラーは2番目のコールバックを受け取ります。これは、プロファイラーがの呼び出しに応答する前に、スレッド B がコールバックを送信するため `JITCachedFunctionSearchStarted` です。 スレッドが呼び出しを行う順序は、スレッドがどのようにスケジュールされているかによって異なります。  
  
 プロファイラーは、重複コールバックを受信するときに、によって参照される値 `pbUseCachedFunction` を、重複するすべてのコールバックについて同じ値に設定する必要があります。 つまり、 `JITCachedFunctionSearchStarted` が同じ値を使用して複数回呼び出された場合、 `functionId` プロファイラーは毎回同じ応答を返す必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
