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
ms.openlocfilehash: a0f5316900dedc6c8983f9e670f60767ed783a40
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84493995"
---
# <a name="stacksnapshotcallback-function"></a>StackSnapshotCallback 関数
[ICorProfilerInfo2::D ostacksnapshot](icorprofilerinfo2-dostacksnapshot-method.md)メソッドによって開始されるスタックウォーク中に、各マネージフレームおよびスタック上のアンマネージフレームの各実行に関する情報をプロファイラーに提供します。  
  
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
 から`COR_PRF_FRAME_INFO`スタックフレームに関する情報を参照する値。 この値は、このコールバック中にのみ使用できます。  
  
 `contextSize`  
 から`CONTEXT`パラメーターによって参照される構造体のサイズ `context` 。  
  
 `context`  
 から`CONTEXT`このフレームの CPU の状態を表す Win32 構造体へのポインター。  
  
 `context`パラメーターは、COR_PRF_SNAPSHOT_CONTEXT フラグが渡された場合にのみ有効です `ICorProfilerInfo2::DoStackSnapshot` 。  
  
 `clientData`  
 からから直接渡されるクライアントデータへのポインター `ICorProfilerInfo2::DoStackSnapshot` 。  
  
## <a name="remarks"></a>解説  
 関数は、 `StackSnapshotCallback` プロファイラーライターによって実装されます。 で実行される作業の複雑さを制限する必要があり `StackSnapshotCallback` ます。 たとえば、を非同期方式で使用する場合、 `ICorProfilerInfo2::DoStackSnapshot` ターゲットスレッドはロックを保持している可能性があります。 内のコードで `StackSnapshotCallback` 同じロックが要求された場合、デッドロックが議論れる可能性があります。  
  
 メソッドは、 `ICorProfilerInfo2::DoStackSnapshot` マネージフレームごとに1回、 `StackSnapshotCallback` またはアンマネージフレームの実行ごとに1回関数を呼び出します。 `StackSnapshotCallback`アンマネージフレームの実行に対してが呼び出された場合、プロファイラーは、(パラメーターによって参照される) レジスタコンテキストを使用して、 `context` 独自のアンマネージスタックウォークを実行できます。 この場合、Win32 `CONTEXT` 構造体は、アンマネージフレームの実行中に最後にプッシュされたフレームの CPU 状態を表します。 Win32 `CONTEXT` 構造体にはすべてのレジスタの値が含まれていますが、スタックポインターレジスタ、フレームポインターレジスタ、命令ポインターレジスタ、および不揮発性 (つまり保持されている) 整数レジスタの値のみに依存する必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [DoStackSnapshot メソッド](icorprofilerinfo2-dostacksnapshot-method.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
