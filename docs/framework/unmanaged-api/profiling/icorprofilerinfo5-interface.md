---
title: ICorProfilerInfo5 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo5
api_location:
- mscorwks.dll
api_type:
- COM
ms.assetid: 7bd48c34-37ed-4230-9eec-39a17280f05d
topic_type:
- apiref
ms.openlocfilehash: 82f6262c2c576b49be4e7fcaa14043950df4c67a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495628"
---
# <a name="icorprofilerinfo5-interface"></a>ICorProfilerInfo5 インターフェイス
[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
 イベント監視を制御するために、コードプロファイラーが共通言語ランタイム (CLR) と通信するために使用するメソッドを提供する[ICorProfilerInfo4](icorprofilerinfo4-interface.md)のサブクラス。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetEventMask2 メソッド](icorprofilerinfo5-geteventmask2-method.md)|プロファイラーが CLR からの通知を受信するための現在のイベント カテゴリーを取得します。|  
|[SetEventMask2 メソッド](icorprofilerinfo5-seteventmask2-method.md)|プロファイラーが CLR からのイベント通知を受信するためのイベントの種類を指定する値を設定します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスで使用できるメソッドは、 [ICorProfilerInfo:: geteventmask](icorprofilerinfo-geteventmask-method.md)メソッドと[ICorProfilerInfo:: seteventmask](icorprofilerinfo-seteventmask-method.md)メソッドを置き換えることを目的としています。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
