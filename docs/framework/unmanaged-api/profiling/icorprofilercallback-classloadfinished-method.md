---
title: ICorProfilerCallback::ClassLoadFinished メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ClassLoadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ClassLoadFinished
helpviewer_keywords:
- ClassLoadFinished method [.NET Framework profiling]
- ICorProfilerCallback::ClassLoadFinished method [.NET Framework profiling]
ms.assetid: 3dd80fbe-d62d-4d4d-acf8-5b7d0efe607e
topic_type:
- apiref
ms.openlocfilehash: 4be2a50664b001e865b5ecdd9aabe8ba727b8c26
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500391"
---
# <a name="icorprofilercallbackclassloadfinished-method"></a>ICorProfilerCallback::ClassLoadFinished メソッド
クラスが読み込みを完了したことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ClassLoadFinished(  
    [in] ClassID classId,  
    [in] HRESULT hrStatus);  
```  
  
## <a name="parameters"></a>パラメーター

- `classId`

  \[in] は、読み込まれたクラスを識別します。

- `hrStatus`

  \[in] クラスが正常に読み込まれたかどうかを示す HRESULT。

## <a name="remarks"></a>解説  
 の値 `classId` は、 `ClassLoadFinished` メソッドが呼び出されるまで、情報要求に対して有効ではありません。  
  
 クラスの読み込みの一部は、コールバック後に続行される場合があり `ClassLoadFinished` ます。 のエラー HRESULT は `hrStatus` エラーを示します。 ただし、の成功 HRESULT は、 `hrStatus` クラスの読み込みの最初の部分が成功したことを示します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [ClassLoadStarted メソッド](icorprofilercallback-classloadstarted-method.md)
