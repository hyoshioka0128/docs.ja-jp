---
title: ICorProfilerCallback::ClassUnloadStarted メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ClassUnloadStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ClassUnloadStarted
helpviewer_keywords:
- ClassUnloadStarted method [.NET Framework profiling]
- ICorProfilerCallback::ClassUnloadStarted method [.NET Framework profiling]
ms.assetid: bc93bead-f3a9-415c-b919-ddd3ca80facc
topic_type:
- apiref
ms.openlocfilehash: 86402abca5386f34256f1f44f674f1e1898ad5fd
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500352"
---
# <a name="icorprofilercallbackclassunloadstarted-method"></a>ICorProfilerCallback::ClassUnloadStarted メソッド
クラスがアンロードされていることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ClassUnloadStarted(  
    [in] ClassID classId);  
```  
  
## <a name="parameters"></a>パラメーター

- `classId`

  \[in] は、アンロードするクラスを識別します。

## <a name="remarks"></a>解説  
 `classId`メソッドから制御が戻った後、の値は情報要求に対して無効です `ClassUnloadStarted` 。このクラスに関する情報を取得するのは、プロファイラーの最後の機会です。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [ClassUnloadFinished メソッド](icorprofilercallback-classunloadfinished-method.md)
