---
title: ICorProfilerCallback::AssemblyUnloadFinished メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AssemblyUnloadFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AssemblyUnloadFinished
helpviewer_keywords:
- AssemblyUnloadFinished method [.NET Framework profiling]
- ICorProfilerCallback::AssemblyUnloadFinished method [.NET Framework profiling]
ms.assetid: 53fca564-84b1-44d4-9e21-17a492d2aae7
topic_type:
- apiref
ms.openlocfilehash: d00e67d29921edc6b7487ceeb12aaa9e9f9bd0ac
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500417"
---
# <a name="icorprofilercallbackassemblyunloadfinished-method"></a>ICorProfilerCallback::AssemblyUnloadFinished メソッド
アセンブリがアンロードされたことをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT AssemblyUnloadFinished(  
    [in] AssemblyID assemblyId,  
    [in] HRESULT    hrStatus);  
```  
  
## <a name="parameters"></a>パラメーター

- `assemblyId`

  \[in] は、アンロードされるアセンブリを識別します。

- `hrStatus`

  \[in] アセンブリが正常にアンロードされたかどうかを示す HRESULT。

## <a name="remarks"></a>解説  
 `assemblyId` [ICorProfilerCallback:: AssemblyUnloadStarted](icorprofilercallback-assemblyunloadstarted-method.md)メソッドがを返すと、の値は情報要求に対して有効ではありません。  
  
 アセンブリのアンロードの一部は、コールバック後に続行される場合があり `AssemblyUnloadFinished` ます。 のエラー HRESULT は `hrStatus` エラーを示します。 ただし、の成功 HRESULT は、 `hrStatus` アセンブリのアンロードの最初の部分が成功したことを示します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
