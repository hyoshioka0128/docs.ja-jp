---
title: ICorProfilerInfo::GetHandleFromThread メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetHandleFromThread
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetHandleFromThread
helpviewer_keywords:
- GetHandleFromThread method [.NET Framework profiling]
- ICorProfilerInfo::GetHandleFromThread method [.NET Framework profiling]
ms.assetid: 36cdc9f5-7579-4cd2-aa36-fc05c741584c
topic_type:
- apiref
ms.openlocfilehash: 419195d9450bf07e5ad8c7cedcac76e175137c96
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84498220"
---
# <a name="icorprofilerinfogethandlefromthread-method"></a>ICorProfilerInfo::GetHandleFromThread メソッド
スレッドの ID を Win32 スレッドハンドルにマップします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetHandleFromThread(  
    [in]  ThreadID threadId,  
    [out] HANDLE  *phThread);  
```  
  
## <a name="parameters"></a>パラメーター  
 `threadId`  
 から割り当てられるスレッド ID。  
  
 `phThread`  
 入出力Win32 スレッドハンドルへのポインター。  
  
## <a name="remarks"></a>解説  
 プロファイラーは、 `DuplicateHandle` 使用する前にハンドルで Win32 関数を呼び出す必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
