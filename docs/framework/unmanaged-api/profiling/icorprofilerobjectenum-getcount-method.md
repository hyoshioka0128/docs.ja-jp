---
title: ICorProfilerObjectEnum::GetCount メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum.GetCount
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum::GetCount
helpviewer_keywords:
- ICorProfilerObjectEnum::GetCount method [.NET Framework profiling]
- GetCount method, ICorProfilerObjectEnum interface [.NET Framework profiling]
ms.assetid: 166b0761-ed80-4ccd-9973-dc20e61bf8fa
topic_type:
- apiref
ms.openlocfilehash: 4c867a9e263f022fc6f8d90a883562e2560ad1b2
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494658"
---
# <a name="icorprofilerobjectenumgetcount-method"></a>ICorProfilerObjectEnum::GetCount メソッド
コレクション内の固定されたオブジェクトの合計数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCount (  
    [out] ULONG   *pcelt  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pcelt`  
 入出力コレクション内の固定されたオブジェクトの数へのポインター。  
  
 このメソッドは、.NET Framework バージョン 3.5 Service Pack 1 (SP1) 以降のバージョンで常に0を返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerObjectEnum インターフェイス](icorprofilerobjectenum-interface.md)
