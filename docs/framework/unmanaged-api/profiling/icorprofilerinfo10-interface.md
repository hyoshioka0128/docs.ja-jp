---
title: ICorProfilerInfo10 インターフェイス
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: 4c5d553744008734037975d6e63e1b07b89cf886
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79175071"
---
# <a name="icorprofilerinfo10-interface"></a>ICorProfilerInfo10 インターフェイス

関数 IL を変更し、ランタイムから情報を照会し、ランタイムを中断および再開するためのメソッドを提供する[ICorProfilerInfo9](icorprofilerinfo9-interface.md)のサブクラス。

## <a name="methods"></a>メソッド  

| Method|説明|  
| ------------|-----------------|  
|[EnumerateObjectReferences メソッド](icorprofilerinfo10-enumerateobjectreferences-method.md)|ObjectID、コールバック、および clientData を指定すると、各オブジェクト参照 (存在する場合) が列挙されます。 |
|[IsFrozenObject メソッド](icorprofilerinfo10-isfrozenobject-method.md)|ObjectID を指定すると、オブジェクトが読み取り専用セグメント内にあるかどうかを判断します。 |
|[GetLOHObjectSizeThreshold メソッド](icorprofilerinfo10-getlohobjectsizethreshold-method.md)|構成済みの LOH しきい値の値を取得します。 |
|[RequestReJITWithInliners メソッド](icorprofilerinfo10-requestrejitwithinliners-method.md)| 要求されたメソッドと、要求されたメソッドのインライナーを REJIT します。  |
|[SuspendRuntime メソッド](icorprofilerinfo10-suspendruntime-method.md)| GC を実行せずにランタイムを中断します。 |
|[ResumeRuntime メソッド](icorprofilerinfo10-resumeruntime-method.md)| GC を実行せずにランタイムを再開します。 |

## <a name="requirements"></a>必要条件  
**プラットフォーム:** NET [Core サポートされるオペレーティング システム](../../../core/install/dependencies.md?pivots=os-windows)を参照してください。  
**ヘッダー** : CorProf.idl、CorProf.h  
**.NET バージョン:**[!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]

## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
