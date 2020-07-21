---
title: ICorProfilerCallback::ModuleLoadFinished メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ModuleLoadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ModuleLoadFinished
helpviewer_keywords:
- ModuleLoadFinished method [.NET Framework profiling]
- ICorProfilerCallback::ModuleLoadFinished method [.NET Framework profiling]
ms.assetid: 050649e5-ffc0-4458-a0a4-d9ee128a219e
topic_type:
- apiref
ms.openlocfilehash: 481fc2c40331e31f6a018d012fb2b2543d4fd9b5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503368"
---
# <a name="icorprofilercallbackmoduleloadfinished-method"></a>ICorProfilerCallback::ModuleLoadFinished メソッド
モジュールが読み込みを終了したことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ModuleLoadFinished(  
    [in] ModuleID moduleId,  
    [in] HRESULT  hrStatus);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleId`  
 から読み込みを終了したモジュールの ID。  
  
 `hrStatus`  
 からモジュールが正常に読み込まれたかどうかを示す HRESULT。  
  
## <a name="remarks"></a>解説  
 の値 `moduleId` は、 `ModuleLoadFinished` メソッドが呼び出されるまで、情報要求に対して有効ではありません。  
  
 モジュールの読み込みの一部は、コールバック後に続行される場合があり `ModuleLoadFinished` ます。 のエラー HRESULT は `hrStatus` エラーを示します。 ただし、の成功 HRESULT は、 `hrStatus` モジュールの読み込みの最初の部分が成功したことを示します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [ModuleLoadStarted メソッド](icorprofilercallback-moduleloadstarted-method.md)
