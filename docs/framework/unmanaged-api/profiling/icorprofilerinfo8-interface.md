---
title: ICorProfilerInfo8 インターフェイス
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: 2cca915eda44d73aea7469e5f752c57309c2300d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495165"
---
# <a name="icorprofilerinfo8-interface"></a>ICorProfilerInfo8 インターフェイス

動的メソッドに関する情報を照会するメソッドを提供する[ICorProfilerInfo7](icorprofilerinfo7-interface.md)のサブクラス。

## <a name="methods"></a>メソッド  

| メソッド|説明|  
| ------------|-----------------|  
|[IsFunctionDynamic メソッド](icorprofilerinfo8-isfunctiondynamic-method.md)| 関数にメタデータが関連付けられていないかどうかを判断します。|
|[GetFunctionFromIP3 メソッド](icorprofilerinfo8-getfunctionfromip3-method.md)| マネージコード命令ポインターを FunctionID にマップします。 このメソッドは、動的メソッドと非動的メソッドの両方に対して機能します。 |
|[GetDynamicFunctionInfo メソッド](icorprofilerinfo8-getdynamicfunctioninfo-method.md)| 動的メソッドに関する情報を取得します。 |

## <a name="requirements"></a>要件  
**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー** : CorProf.idl、CorProf.h  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  

## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
