---
title: ICorProfilerInfo7 インターフェイス
ms.date: 03/30/2017
ms.assetid: cf37c462-73c5-412a-a7f8-bb26ca746313
ms.openlocfilehash: 0e9f76717aeff27e863245faac241927e7495076
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84495490"
---
# <a name="icorprofilerinfo7-interface"></a>ICorProfilerInfo7 インターフェイス
[.NET Framework 4.6.1 以降のバージョンでのみでサポート]  
  
 新しく定義されたメタデータをモジュールに適用し、メモリ内シンボルストリームへのアクセスを提供するメソッドを提供する[ICorProfilerInfo6](icorprofilerinfo6-interface.md)のサブクラスです。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ApplyMetaData メソッド](icorprofilerinfo7-applymetadata-method.md)|メソッドによって新たに定義されたメタデータ `IMetadataEmit::Define*` を、指定したモジュールに適用します。|  
|[GetInMemorySymbolsLength メソッド](icorprofilerinfo7-getinmemorysymbolslength-method.md)|メモリ内シンボルストリームの長さを返します。|  
|[ReadInMemorySymbols](icorprofilerinfo7-readinmemorysymbols.md)|メモリ内シンボルストリームからバイトを読み取ります。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
