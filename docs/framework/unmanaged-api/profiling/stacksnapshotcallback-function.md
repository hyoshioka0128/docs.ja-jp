---
title: StackSnapshotCallback 関数
ms.date: 03/30/2017
api_name:
- StackSnapshotCallback
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- StackSnapshotCallback
helpviewer_keywords:
- StackSnapshotCallback function [.NET Framework profiling]
ms.assetid: d0f235b2-91fe-4f82-b7d5-e5c64186eea8
topic_type:
- apiref
ms.openlocfilehash: c0cec9eb7bb8bbc94b255152a9b4d79108bdd1b1
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74427082"
---
# <a name="stacksnapshotcallback-function"></a>StackSnapshotCallback 関数
[ICorProfilerInfo2::D ostacksnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)メソッドによって開始されるスタックウォーク中に、各マネージフレームおよびスタック上のアンマネージフレームの各実行に関する情報をプロファイラーに提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT __stdcall StackSnapshotCallback (  
    [in] FunctionID funcId,  
    [in] UINT_PTR ip,  
    [in] COR_PRF_FRAME_INFO frameInfo,  
    [in] ULONG32 contextSize,  
    [in] BYTE context[],  
    [in] void *clientData  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `funcId`  
 からこの値が0の場合、このコールバックはアンマネージフレームの実行用です。それ以外の場合は、マネージ関数の識別子であり、このコールバックはマネージフレーム用です。  
  
 `ip`  
 からフレーム内のネイティブコード命令ポインターの値。  
  
 `frameInfo`  
 からスタックフレームに関する情報を参照する `COR_PRF_FRAME_INFO` 値。 この値は、このコールバック中にのみ使用できます。  
  
 `contextSize`  
 から`context` パラメーターによって参照される `CONTEXT` 構造体のサイズ。  
  
 `context`  
 からこのフレームの CPU の状態を表す Win32 `CONTEXT` 構造体へのポインター。  
  
 `context` パラメーターは `ICorProfilerInfo2::DoStackSnapshot`で COR_PRF_SNAPSHOT_CONTEXT フラグが渡された場合にのみ有効です。  
  
 `clientData`  
 から`ICorProfilerInfo2::DoStackSnapshot`から直接渡されるクライアントデータへのポインター。  
  
## <a name="remarks"></a>コメント  
 `StackSnapshotCallback` 関数は、プロファイラーライターによって実装されます。 `StackSnapshotCallback`で実行する作業の複雑さを制限する必要があります。 たとえば、非同期方式で `ICorProfilerInfo2::DoStackSnapshot` を使用する場合、ターゲットスレッドがロックを保持している可能性があります。 `StackSnapshotCallback` 内のコードで同じロックが要求された場合、デッドロックが発生する可能性があります。  
  
 `ICorProfilerInfo2::DoStackSnapshot` メソッドは、マネージフレームごとに1回、またはアンマネージフレームの実行ごとに1回、`StackSnapshotCallback` 関数を呼び出します。 アンマネージフレームの実行に対して `StackSnapshotCallback` が呼び出された場合、プロファイラーは、(`context` パラメーターによって参照される) レジスタコンテキストを使用して、独自のアンマネージスタックウォークを実行できます。 この場合、Win32 `CONTEXT` 構造体は、アンマネージフレームの実行中に最後にプッシュされたフレームの CPU 状態を表します。 Win32 `CONTEXT` 構造体にはすべてのレジスタの値が含まれていますが、スタックポインターレジスタ、フレームポインターレジスタ、命令ポインターレジスタ、および不揮発性の (つまり、保持されている) 整数レジスタの値のみに依存する必要があります。  
  
## <a name="requirements"></a>要件  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>参照

- [DoStackSnapshot メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)
- [グローバル静的関数のプロファイル](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
