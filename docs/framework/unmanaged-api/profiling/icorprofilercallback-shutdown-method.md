---
title: ICorProfilerCallback::Shutdown メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.Shutdown
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::Shutdown
helpviewer_keywords:
- ICorProfilerCallback::Shutdown method [.NET Framework profiling]
- Shutdown method [.NET Framework profiling]
ms.assetid: 1ea194f0-a331-4855-a2ce-37393b8e5f84
topic_type:
- apiref
ms.openlocfilehash: f6873de1a864489d144a671b1a9e1349eaf77d15
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503184"
---
# <a name="icorprofilercallbackshutdown-method"></a>ICorProfilerCallback::Shutdown メソッド
アプリケーションがシャットダウン中であることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Shutdown();  
```  
  
## <a name="remarks"></a>解説  
 プロファイラーコードは、メソッドが呼び出された後に、 [ICorProfilerInfo](icorprofilerinfo-interface.md)インターフェイスのメソッドを安全に呼び出すことができません `Shutdown` 。 メソッドを呼び出す `ICorProfilerInfo` と、メソッドから制御が戻った後に、未定義の動作が発生し `Shutdown` ます。 シャットダウン後も、特定の不変イベントが発生する可能性があります。プロファイラーは、このようになるとすぐに制御を戻す必要があります。  
  
 メソッドは、 `Shutdown` プロファイリングされているマネージアプリケーションがマネージコードとして開始されている場合にのみ呼び出されます (つまり、プロセススタックの初期フレームが管理されます)。 アプリケーションがアンマネージコードとして起動され、後でマネージコードにジャンプし、その結果、共通言語ランタイム (CLR) のインスタンスを作成した場合、 `Shutdown` は呼び出されません。 このような場合、プロファイラーは、DLL_PROCESS_DETACH 値を使用してリソースを解放し、 `DllMain` トレースをディスクにフラッシュするなどのデータのクリーンアップ処理を実行するルーチンをライブラリに組み込む必要があります。  
  
 一般に、プロファイラーは予期しないシャットダウンに対処する必要があります。 たとえば、Win32's `TerminateProcess` メソッド (Winbase. h で宣言) によってプロセスが停止される場合があります。 それ以外の場合、CLR は、特定のマネージスレッド (バックグラウンドスレッド) を停止します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [Initialize メソッド](icorprofilercallback-initialize-method.md)
