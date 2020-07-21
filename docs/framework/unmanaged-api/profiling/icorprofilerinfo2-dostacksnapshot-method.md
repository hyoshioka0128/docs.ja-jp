---
title: ICorProfilerInfo2::DoStackSnapshot メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.DoStackSnapshot
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::DoStackSnapshot
helpviewer_keywords:
- ICorProfilerInfo2::DoStackSnapshot method [.NET Framework profiling]
- DoStackSnapshot method [.NET Framework profiling]
ms.assetid: 287b11e9-7c52-4a13-ba97-751203fa97f4
topic_type:
- apiref
ms.openlocfilehash: b9a7142de01d818390b740a795f70a4606952780
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497375"
---
# <a name="icorprofilerinfo2dostacksnapshot-method"></a>ICorProfilerInfo2::DoStackSnapshot メソッド
指定したスレッドのスタック上のマネージフレームをウォークし、コールバックを介してプロファイラーに情報を送信します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DoStackSnapshot(  
    [in] ThreadID thread,  
    [in] StackSnapshotCallback *callback,  
    [in] ULONG32 infoFlags,  
    [in] void *clientData,  
    [in, size_is(contextSize), length_is(contextSize)] BYTE context[],  
    [in] ULONG32 contextSize);  
```  
  
## <a name="parameters"></a>パラメーター  
 `thread`  
 からターゲットスレッドの ID。  
  
 に null を渡すと `thread` 、現在のスレッドのスナップショットが生成されます。 `ThreadID`別のスレッドのが渡された場合、共通言語ランタイム (CLR) はそのスレッドを中断し、スナップショットを実行して、再開します。  
  
 `callback`  
 から[Stacksnapshotcallback](stacksnapshotcallback-function.md)メソッドの実装へのポインター。プロファイラーは、各マネージフレームと、アンマネージフレームの各実行に関する情報を提供するために、CLR によって呼び出されます。  
  
 メソッドは、 `StackSnapshotCallback` プロファイラーライターによって実装されます。  
  
 `infoFlags`  
 からによって各フレームに返されるデータ量を指定する[COR_PRF_SNAPSHOT_INFO](cor-prf-snapshot-info-enumeration.md)列挙体の値 `StackSnapshotCallback` 。  
  
 `clientData`  
 からクライアントデータへのポインター。これは、コールバック関数に直接渡され `StackSnapshotCallback` ます。  
  
 `context`  
 からスタックウォークをシード処理するために使用される Win32 構造体へのポインター `CONTEXT` 。 Win32 構造体には、 `CONTEXT` cpu レジスタの値が含まれており、特定の時点における cpu の状態を表します。  
  
 スタックの最上位がアンマネージヘルパーコードの場合、このシードを使用すると、CLR はスタックウォークの開始位置を決定できます。それ以外の場合、シードは無視されます。 非同期ウォークにはシードを指定する必要があります。 同期ウォークを実行する場合、シードは必要ありません。  
  
 パラメーターは、 `context` パラメーターで COR_PRF_SNAPSHOT_CONTEXT フラグが渡された場合にのみ有効です `infoFlags` 。  
  
 `contextSize`  
 から`CONTEXT`パラメーターによって参照される構造体のサイズ `context` 。  
  
## <a name="remarks"></a>解説  
 に null を渡す `thread` と、現在のスレッドのスナップショットが生成されます。 スナップショットは、その時点でターゲットスレッドが中断されている場合にのみ、他のスレッドで取得できます。  
  
 プロファイラーがスタックをウォークする場合は、を呼び出し `DoStackSnapshot` ます。 その呼び出しから CLR が戻る前に、 `StackSnapshotCallback` スタック上のマネージフレーム (またはアンマネージフレームの実行) ごとに、を複数回呼び出します。 アンマネージフレームが検出されたら、それらを自分で調べる必要があります。  
  
 スタックがウォークされる順序は、フレームがスタックにプッシュされた方法と逆になります。リーフ (最後にプッシュされた) フレームは、最初にメイン (最初にプッシュされた) フレームに最後に配置されます。  
  
 プロファイラーをプログラミングしてマネージスタックをウォークする方法の詳細については、「 [.NET Framework 2.0: 基本およびそれ以降のプロファイラースタックウォーク](https://docs.microsoft.com/previous-versions/dotnet/articles/bb264782(v=msdn.10))」を参照してください。  
  
 次のセクションで説明するように、スタックウォークは同期または非同期にすることができます。  
  
## <a name="synchronous-stack-walk"></a>同期スタックウォーク  
 同期スタックウォークでは、コールバックへの応答として現在のスレッドのスタックを調べる必要があります。 シード処理や中断を必要としません。  
  
 プロファイラーの[ICorProfilerCallback](icorprofilercallback-interface.md) (または[ICorProfilerCallback2](icorprofilercallback2-interface.md)) メソッドのいずれかを呼び出す CLR に応答してを呼び出す場合は、を呼び出して、 `DoStackSnapshot` 現在のスレッドのスタックをウォークします。 これは、 [ICorProfilerCallback:: ObjectAllocated](icorprofilercallback-objectallocated-method.md)などの通知でスタックがどのように見えるかを確認する場合に便利です。 メソッド内からを呼び出すだけで `DoStackSnapshot` `ICorProfilerCallback` 、パラメーターとパラメーターで null を渡すことができ `context` `thread` ます。  
  
## <a name="asynchronous-stack-walk"></a>非同期スタックウォーク  
 非同期スタックウォークでは、別のスレッドのスタックを調べたり、コールバックに応答せずに現在のスレッドの命令ポインターをハイジャックしたりして、現在のスレッドのスタックを調べます。 スタックの最上位が、プラットフォーム呼び出し (PInvoke) または COM 呼び出しの一部ではなく、CLR 自体のヘルパーコードであるアンマネージコードである場合、非同期ウォークにはシードが必要です。 たとえば、ジャストインタイム (JIT) コンパイルまたはガベージコレクションを実行するコードは、ヘルパーコードです。  
  
 最上位のマネージフレームが見つかるまで、ターゲットスレッドを直接中断し、自分でスタックを調査することで、シードを取得します。 ターゲットスレッドが中断された後、ターゲットスレッドの現在のレジスタコンテキストを取得します。 次に、 [ICorProfilerInfo:: GetFunctionFromIP](icorprofilerinfo-getfunctionfromip-method.md)を呼び出すことによって、登録コンテキストがアンマネージコードを指しているかどうかを確認します。0と等しいを返す場合 `FunctionID` 、フレームはアンマネージコードです。 次に、最初のマネージフレームに達するまでスタックをウォークし、そのフレームのレジスタコンテキストに基づいてシードコンテキストを計算します。  
  
 `DoStackSnapshot`シードコンテキストでを呼び出して、非同期スタックウォークを開始します。 シードを指定しないと、では `DoStackSnapshot` スタックの一番上にあるマネージフレームがスキップされ、その結果、不完全なスタックウォークが発生します。 シードを指定する場合は、JIT コンパイルまたはネイティブイメージジェネレーター (Ngen.exe) で生成されたコードをポイントする必要があります。それ以外の場合は、 `DoStackSnapshot` エラーコード CORPROF_E_STACKSNAPSHOT_UNMANAGED_CTX を返します。  
  
 非同期スタックウォークは、次のガイドラインに従っている場合を除き、デッドロックまたはアクセス違反を簡単に引き起こすことができます。  
  
- スレッドを直接中断する場合は、マネージコードを実行していないスレッドだけが別のスレッドを中断できることに注意してください。  
  
- [ICorProfilerCallback:: ThreadDestroyed](icorprofilercallback-threaddestroyed-method.md)コールバックは、そのスレッドのスタックウォークが完了するまで常にブロックします。  
  
- プロファイラーがガベージコレクションをトリガーできる CLR 関数を呼び出している間は、ロックを保持しないでください。 つまり、所有スレッドがガベージコレクションをトリガーする呼び出しを行う場合は、ロックを保持しません。  
  
 また、 `DoStackSnapshot` プロファイラーによって作成されたスレッドからを呼び出した場合に、別のターゲットスレッドのスタックを調べることができるように、デッドロックのリスクもあります。 最初に作成したスレッドが特定の `ICorProfilerInfo*` メソッド (を含む) を入力すると、clr はスレッド `DoStackSnapshot` ごとに clr 固有の初期化を実行します。 プロファイラーが、ウォークしようとしているスタックを持つターゲットスレッドを中断し、そのターゲットスレッドがこのスレッドごとの初期化を実行するために必要なロックを所有していた場合、デッドロックが発生します。 このデッドロックを回避するには、プロファイラーによっ `DoStackSnapshot` て作成されたスレッドからへの最初の呼び出しを行い、個別のターゲットスレッドをウォークしますが、先にターゲットスレッドを中断しないようにします。 この最初の呼び出しにより、スレッドごとの初期化がデッドロックなしで完了することが保証されます。 が `DoStackSnapshot` 成功し、少なくとも1つのフレームを報告した場合は、その時点以降に、プロファイラーによって作成されたスレッドは、任意のターゲットスレッドを中断し、を呼び出して `DoStackSnapshot` ターゲットスレッドのスタックをたどることができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
