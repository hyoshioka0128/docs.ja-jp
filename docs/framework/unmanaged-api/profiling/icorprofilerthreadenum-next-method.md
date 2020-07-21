---
title: ICorProfilerThreadEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerThreadEnum.Next
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerThreadEnum::Next
helpviewer_keywords:
- ICorProfilerThreadEnum::Next method [.NET Framework profiling]
- Next method, ICorProfilerThreadEnum interface [.NET Framework profiling]
ms.assetid: f3535279-3c63-41a2-ab0e-a129dc5a01e8
topic_type:
- apiref
ms.openlocfilehash: 37d1acfa70a1a2b2c18fb34fb5d6024f3b61e2ab
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494346"
---
# <a name="icorprofilerthreadenumnext-method"></a>ICorProfilerThreadEnum::Next メソッド
スレッドのシーケンシャル コレクションから、列挙子の現在の位置以降にある指定した数の隣接するスレッドを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next (    [in]  ULONG      celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
                    ThreadID ids[],  
    [out] ULONG *   pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 [in] 取得するスレッドの数。  
  
 `ids`  
 [out] `ThreadID` 値の配列。それぞれの値は、取得されたスレッドを表します。  
  
 `pceltFetched`  
 [out] `ids` 配列で実際に返されるスレッドの数へのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`celt` 要素が返されました。|  
|S_FALSE|`celt` よりも少ない数の要素が返されました。これは、列挙が完了したことを示します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerThreadEnum インターフェイス](icorprofilerthreadenum-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
