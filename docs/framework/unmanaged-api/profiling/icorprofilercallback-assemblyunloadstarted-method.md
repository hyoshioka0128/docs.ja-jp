---
title: ICorProfilerCallback::AssemblyUnloadStarted メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AssemblyUnloadStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AssemblyUnloadStarted
helpviewer_keywords:
- ICorProfilerCallback::AssemblyUnloadStarted method [.NET Framework profiling]
- AssemblyUnloadStarted method [.NET Framework profiling]
ms.assetid: 6e47b7e5-0335-4dd3-8c42-d3c07d62b102
topic_type:
- apiref
ms.openlocfilehash: 80054a8292c69b957664cb3573b0a8694c7f9fd2
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500404"
---
# <a name="icorprofilercallbackassemblyunloadstarted-method"></a>ICorProfilerCallback::AssemblyUnloadStarted メソッド
アセンブリがアンロードされていることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT AssemblyUnloadStarted(  
    [in] AssemblyID assemblyId);  
```  
  
## <a name="parameters"></a>パラメーター

- `assemblyId`

  \[in] は、アンロードされるアセンブリを識別します。

## <a name="remarks"></a>解説  
 `assemblyId`メソッドから制御が戻った後、の値は情報要求に対して無効です `AssemblyUnloadStarted` 。これは、このアセンブリに関する情報を取得する最後の機会です。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [AssemblyUnloadFinished メソッド](icorprofilercallback-assemblyunloadfinished-method.md)
