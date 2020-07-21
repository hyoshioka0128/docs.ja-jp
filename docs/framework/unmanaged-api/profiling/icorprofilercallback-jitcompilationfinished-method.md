---
title: ICorProfilerCallback::JITCompilationFinished メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.JITCompilationFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::JITCompilationFinished
helpviewer_keywords:
- JITCompilationFinished method [.NET Framework profiling]
- ICorProfilerCallback::JITCompilationFinished method [.NET Framework profiling]
ms.assetid: 8dcd7537-d0c6-498c-8a56-2c060310ef65
topic_type:
- apiref
ms.openlocfilehash: 0da67f0d4be779cc21481d03a21209620289888e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500061"
---
# <a name="icorprofilercallbackjitcompilationfinished-method"></a>ICorProfilerCallback::JITCompilationFinished メソッド
Just-in-time (JIT) コンパイラが関数のコンパイルを完了したことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT JITCompilationFinished(  
    [in] FunctionID functionId,  
    [in] HRESULT    hrStatus,  
    [in] BOOL       fIsSafeToBlock);  
```  
  
## <a name="parameters"></a>パラメーター

- `functionId`

  \[in] コンパイルされた関数の ID。

- `hrStatus`

  \[in] コンパイルが成功したかどうかを示す値。

- `fIsSafeToBlock`

  \[in] プロファイラーに対して、ブロックがランタイムの操作に影響を与えるかどうかを示す値。 この値は、ブロックによって、 `true` ランタイムが呼び出し元のスレッドがこのコールバックから戻るのを待機する場合は、それ以外の場合はです `false` 。

  の値は `true` ランタイムに害を及ぼすことはありませんが、プロファイルの結果をスキューできます。

## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [JITCompilationStarted メソッド](icorprofilercallback-jitcompilationstarted-method.md)
