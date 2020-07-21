---
title: ICorProfilerCallback5 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback5
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback5
helpviewer_keywords:
- ICorProfilerCallback5 interface [.NET Framework profiling]
ms.assetid: 61d2e9ef-5f1f-4771-8847-239616e35d84
topic_type:
- apiref
ms.openlocfilehash: 02a690503d7b6323f19dcb66247d8a552b760b1c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499208"
---
# <a name="icorprofilercallback5-interface"></a>ICorProfilerCallback5 インターフェイス
[ICorProfilerCallback:: RootReferences](icorprofilercallback-rootreferences-method.md)メソッドまたは[ICorProfilerCallback2:: RootReferences2](icorprofilercallback2-rootreferences2-method.md)メソッドと共に[ICorProfilerCallback:: ObjectReferences](icorprofilercallback-objectreferences-method.md)メソッドと[conditional tableelementreferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md)メソッドと共に使用する場合に、プロファイラーがライブオブジェクトの完全なクロージャを識別するのに役立つ補足情報を提供します。  
  
 `ICorProfilerCallback5` は、依存ハンドルに関連する通知をサブスクライブするために、マネージド メモリ プロファイラーによって実装される必要があります。  
  
## <a name="remarks"></a>解説  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ConditionalWeakTableElementReferences メソッド](icorprofilercallback5-conditionalweaktableelementreferences-method.md)|直接のメンバー フィールド参照および `ConditionalWeakTable` 依存を介してこれらのルーツによって参照されるオブジェクトの推移的終了を識別します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [ICorProfilerCallback2 インターフェイス](icorprofilercallback2-interface.md)
