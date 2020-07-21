---
title: ICorProfilerCallback::Initialize メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.Initialize
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::Initialize
helpviewer_keywords:
- Initialize method, ICorProfilerCallback interface [.NET Framework profiling]
- ICorProfilerCallback::Initialize method [.NET Framework profiling]
ms.assetid: dc5fab2a-4b45-4b12-8727-b89c9915f23e
topic_type:
- apiref
ms.openlocfilehash: ea4fc8ab39d616415106150f56f4b7afd5f68237
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500105"
---
# <a name="icorprofilercallbackinitialize-method"></a>ICorProfilerCallback::Initialize メソッド
新しい共通言語ランタイム (CLR) アプリケーションが開始されるたびに、コードプロファイラーを初期化するために呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Initialize(  
    [in] IUnknown     *pICorProfilerInfoUnk);  
```  
  
## <a name="parameters"></a>パラメーター

- `pICorProfilerInfoUnk`

  \[in) プロファイラーが[ICorProfilerInfo](icorprofilerinfo-interface.md)インターフェイスポインターを照会する必要がある[IUnknown](/cpp/atl/iunknown)インターフェイスへのポインター。  

## <a name="remarks"></a>解説  
 `Initialize`呼び出しは、変更できないコールバックを有効 (または無効) にする唯一の機会です。 呼び出しによってコールバックが有効になると `Initialize` 、後で[ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md)を使用して無効にすることはできません。 [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)列挙の COR_PRF_MONITOR_IMMUTABLE 値は、どのイベントが不変であるかを示します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [Shutdown メソッド](icorprofilercallback-shutdown-method.md)
