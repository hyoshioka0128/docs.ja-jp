---
title: 'ICorProfilerCallback7:: Moduleinmemory メソッド'
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback7.ModuleInMemorySymbolsUpdated
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.assetid: f362a896-3247-4894-9727-e48dbbcd2c78
ms.openlocfilehash: c7e53816c2f571fe6ff68b517ed827459a0f1562
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499091"
---
# <a name="icorprofilercallback7moduleinmemorysymbolsupdated-method"></a>ICorProfilerCallback7:: Moduleinmemory メソッド
[.NET Framework 4.6.1 以降のバージョンでのみでサポート]  
  
 メモリ内モジュールに関連付けられているシンボルストリームが更新されるたびに、プロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ModuleInMemorySymbolsUpdated(  
     ModuleID moduleId  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 [入力] `moduleId`  
 シンボルストリームが更新されるメモリ内モジュールの識別子。  
  
## <a name="remarks"></a>解説  
 このコールバックは、 [ICorProfilerCallback5:: SetEventMask2](icorprofilerinfo5-seteventmask2-method.md)メソッドを呼び出すときに、 [COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED](cor-prf-high-monitor-enumeration.md)イベントマスクフラグを設定することによって制御されます。  
  
> [!NOTE]
> このイベントは、api を使用して暗黙的に作成または変更されたシンボルに対しては、現在発生していません <xref:System.Reflection.Emit> 。  
  
 アセンブリのシンボルを指定する引数を含むマネージメソッドのオーバーロードのいずれかを呼び出すことによって、シンボルが事前に提供されていても <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> `rawSymbolStore` 、 [moduleloadfinished](icorprofilercallback-moduleloadfinished-method.md)コールバックが発生するまで、ランタイムはシンボリックデータをモジュールに実際に関連付けない場合があります。 このイベントは、後でこのようなモジュールのシンボルを収集する機会を提供します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ModuleLoadFinished メソッド](icorprofilercallback-moduleloadfinished-method.md)
- [SetEventMask2 メソッド](icorprofilerinfo5-seteventmask2-method.md)
- [ICorProfilerCallback7 インターフェイス](icorprofilercallback7-interface.md)
