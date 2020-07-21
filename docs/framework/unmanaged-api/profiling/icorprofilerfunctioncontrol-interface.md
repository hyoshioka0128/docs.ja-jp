---
title: ICorProfilerFunctionControl インターフェイス
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl
helpviewer_keywords:
- ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: 4e3d3141-4662-4166-8f05-bc857c1b4216
topic_type:
- apiref
ms.openlocfilehash: 177127c8c53e4fee31f7007d04c49cc337cca458
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84498727"
---
# <a name="icorprofilerfunctioncontrol-interface"></a>ICorProfilerFunctionControl インターフェイス
特定のメソッドを再コンパイルする時に JIT コンパイラーがコードをどのように生成するかを制御するために、コード プロファイラーが共通言語ランタイム (CLR) と通信できるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[SetCodegenFlags メソッド](icorprofilerfunctioncontrol-setcodegenflags-method.md)|[COR_PRF_CODEGEN_FLAGS](cor-prf-codegen-flags-enumeration.md)列挙型の1つ以上のフラグを設定して、JUST-IN-TIME (JIT) 再コンパイル関数のコード生成を制御します。|  
|[SetILFunctionBody メソッド](icorprofilerfunctioncontrol-setilfunctionbody-method.md)|メソッドの中間共通言語 (CIL) 本体を置換します。|  
|[SetILInstrumentedCodeMap メソッド](icorprofilerfunctioncontrol-setilinstrumentedcodemap-method.md)|指定した共通中間言語 (CIL) マップ エントリを使用して、指定される関数のコード マップを設定します。|  
  
## <a name="remarks"></a>解説  
 `ICorProfilerFunctionControl` インターフェイスは、単一の再コンパイルされた関数に対してコード生成を制御するためにメソッドを提供します。 プロファイラーは、 [ICorProfilerCallback4:: GetReJITParameters](icorprofilercallback4-getrejitparameters-method.md)コールバックを使用して、このインターフェイスのインスタンスを取得します。 `ICorProfilerFunctionControl` の各インスタンスは一つの関数の全てのインスタンスを制御します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo4 インターフェイス](icorprofilerinfo4-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [EnumJITedFunctions2 メソッド](icorprofilerinfo4-enumjitedfunctions2-method.md)
