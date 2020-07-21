---
title: ICorProfilerCallback::JITCompilationStarted メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCompilationStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCompilationStarted
helpviewer_keywords:
- JITCompilationStarted method [.NET Framework profiling]
- ICorProfilerCallback::JITCompilationStarted method [.NET Framework profiling]
ms.assetid: 31782b36-d311-4518-8f45-25f65385af5b
topic_type:
- apiref
ms.openlocfilehash: 57981ef134dc3f30337d47f5cee426a25d0414cf
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500040"
---
# <a name="icorprofilercallbackjitcompilationstarted-method"></a>ICorProfilerCallback::JITCompilationStarted メソッド
Just-in-time (JIT) コンパイラが関数のコンパイルを開始したことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT JITCompilationStarted(  
    [in] FunctionID functionId,  
    [in] BOOL       fIsSafeToBlock);  
```  
  
## <a name="parameters"></a>パラメーター  
 `functionId`  
 からコンパイルを開始する関数の ID。  
  
 `fIsSafeToBlock`  
 からプロファイラーに対して、ブロックがランタイムの操作に影響を与えるかどうかを示す値。 この値は、ブロックによって、 `true` ランタイムが呼び出し元のスレッドがこのコールバックから戻るのを待機する場合は、それ以外の場合はです `false` 。  
  
 の値は `true` ランタイムに害を及ぼすことはありませんが、プロファイルの結果をスキューできます。  
  
## <a name="remarks"></a>解説  
 ランタイムがクラスコンストラクターを処理する方法によって、各関数に対して複数のペアの `JITCompilationStarted` と[ICorProfilerCallback:: JITCompilationFinished](icorprofilercallback-jitcompilationfinished-method.md)呼び出しを受け取ることができます。 たとえば、ランタイムは JIT コンパイルメソッド A を開始しますが、クラス B のクラスコンストラクターを実行する必要があります。 このため、ランタイムは、クラス B のコンストラクターを JIT でコンパイルして実行します。 コンストラクターが実行されている間、メソッド a が呼び出されます。これにより、メソッド A が再度 JIT コンパイルされます。 このシナリオでは、メソッド A の最初の JIT コンパイルが停止します。 ただし、JIT コンパイルメソッド A の両方の試行は、JIT コンパイルイベントを使用して報告されます。 プロファイラーは、 [ICorProfilerInfo:: SetILFunctionBody](icorprofilerinfo-setilfunctionbody-method.md)メソッドを呼び出すことによってメソッド A の Microsoft 中間言語 (MSIL) コードを置き換える必要がある場合、両方のイベントに対してこれを行う必要があり `JITCompilationStarted` ますが、両方に同じ msil ブロックを使用する場合があります。  
  
 2つのスレッドが同時にコールバックを作成する場合、プロファイラーは JIT コールバックのシーケンスをサポートする必要があります。 たとえば、スレッド A はを呼び出し `JITCompilationStarted` ます。 ただし、スレッド A が呼び出される前に、スレッド B は、 `JITCompilationFinished` スレッド a のコールバックからの関数 ID を使用して[ICorProfilerCallback:: ExceptionSearchFunctionEnter](icorprofilercallback-exceptionsearchfunctionenter-method.md)を呼び出し `JITCompilationStarted` ます。 の呼び出しが `JITCompilationFinished` まだプロファイラーによって受信されていないため、関数 ID がまだ有効ではないように見えることがあります。 ただし、このような場合は、関数 ID が有効です。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [JITCompilationFinished メソッド](icorprofilercallback-jitcompilationfinished-method.md)
