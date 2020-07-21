---
title: COR_PRF_HIGH_MONITOR 列挙型
ms.date: 04/10/2018
ms.assetid: 3ba543d8-15e5-4322-b6e7-1ebfc92ed7dd
ms.openlocfilehash: b813b32ef4522f1707812d337d20790ce75f3d55
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500846"
---
# <a name="cor_prf_high_monitor-enumeration"></a>COR_PRF_HIGH_MONITOR 列挙型

[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
プロファイラーが読み込み時に[ICorProfilerInfo5:: SetEventMask2](icorprofilerinfo5-seteventmask2-method.md)メソッドに対して指定できる、 [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)列挙に含まれるフラグだけでなく、フラグも提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef enum {  
    COR_PRF_HIGH_MONITOR_NONE                     = 0x00000000,  
    COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES          = 0x00000001,  
    COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED        = 0x00000002,
    COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS = 0x00000004,
    COR_PRF_HIGH_DISABLE_TIERED_COMPILATION       = 0x00000008,
    COR_PRF_HIGH_BASIC_GC                         = 0x00000010,
    COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS         = 0x00000020,
    COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED    = 0x00000040,
    COR_PRF_HIGH_REQUIRE_PROFILE_IMAGE            = 0,  
    COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH           = COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED |
                                                    COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS |
                                                    COR_PRF_HIGH_BASIC_GC |
                                                    COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS |
                                                    COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED,  
    COR_PRF_HIGH_MONITOR_IMMUTABLE                = COR_PRF_HIGH_DISABLE_TIERED_COMPILATION  
} COR_PRF_HIGH_MONITOR;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`COR_PRF_HIGH_MONITOR_NONE`|フラグが設定されていません。|  
|`COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES`|CLR アセンブリ参照クロージャウォーク中にアセンブリ参照を追加するための[ICorProfilerCallback6:: GetAssemblyReference](icorprofilercallback6-getassemblyreferences-method.md)コールバックを制御します。|  
|`COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED`|メモリ内モジュールに関連付けられているシンボルストリームに更新するための[ICorProfilerCallback7:: Moduleinmemorysymbol supcallback](icorprofilercallback7-moduleinmemorysymbolsupdated-method.md)を制御します。|  
|`COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS`|動的メソッドがガベージコレクションおよびアンロードされたことを示す[ICorProfilerCallback9::D ynamicmethodunloaded](icorprofilercallback9-dynamicmethodunloaded-method.md)コールバックを制御します。 <br/> [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]|
|`COR_PRF_HIGH_DISABLE_TIERED_COMPILATION`|.NET Core 3.0 以降のバージョンのみ: プロファイラーの階層化された[コンパイル](../../../core/whats-new/dotnet-core-3-0.md)を無効にします。|
|`COR_PRF_HIGH_BASIC_GC`|.NET Core 3.0 以降のバージョンのみ: と比較して、軽量の GC プロファイルオプションが用意されて [`COR_PRF_MONITOR_GC`](cor-prf-monitor-enumeration.md) います。 [GarbageCollectionStarted](icorprofilercallback2-garbagecollectionstarted-method.md)、 [GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)、および[GetGenerationBounds](icorprofilerinfo2-getgenerationbounds-method.md)の各コールバックのみを制御します。 フラグとは異なり `COR_PRF_MONITOR_GC` 、 `COR_PRF_HIGH_BASIC_GC` は同時実行ガベージコレクションを無効にしません。|
|`COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS`|.NET Core 3.0 以降のバージョンのみ: Gc を圧縮するために、 [Movedreferences](icorprofilercallback-movedreferences-method.md)と[MovedReferences2](icorprofilercallback4-movedreferences2-method.md)コールバックを有効にします。|
|`COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED`|.NET Core 3.0 以降のバージョンのみ: に似て [`COR_PRF_MONITOR_OBJECT_ALLOCATED`](cor-prf-monitor-enumeration.md) いますが、ラージオブジェクトヒープ (LOH) に対してのみオブジェクト割り当てに関する情報を提供します。|
|`COR_PRF_HIGH_REQUIRE_PROFILE_IMAGE`|プロファイルが強化されたイメージを必要とするすべての `COR_PRF_HIGH_MONITOR` フラグを表しています。 これは、 `COR_PRF_REQUIRE_PROFILE_IMAGE` [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)列挙のフラグに対応します。|  
|`COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH`|プロファイラーが実行中のアプリケーションに割り当てられた後に設定することが可能な、`COR_PRF_HIGH_MONITOR` のすべてのフラグを表します。|  
|`COR_PRF_HIGH_MONITOR_IMMUTABLE`|初期化中にのみ設定可能な、`COR_PRF_HIGH_MONITOR` のすべてのフラグを表します。 他の場所でこれらのフラグを変更しようとすると、エラーを表す `HRESULT` 値が生じます。|  
  
## <a name="remarks"></a>解説

`COR_PRF_HIGH_MONITOR`フラグは、 `pdwEventsHigh` [ICorProfilerInfo5:: GetEventMask2](icorprofilerinfo5-geteventmask2-method.md)メソッドと[ICorProfilerInfo5:: SetEventMask2](icorprofilerinfo5-seteventmask2-method.md)メソッドのパラメーターと共に使用されます。  
  
.NET Framework 4.6.1 以降では、の値が `COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH` 0 から (0x00000002) に変更されました `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` 。 .NET Framework 4.7.2 以降では、値がからに変更されました `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED | COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS` 。

`COR_PRF_HIGH_MONITOR_IMMUTABLE`は、初期化中にのみ設定できるすべてのフラグを表すビットマスクであることを意図しています。 これらのフラグを他の場所で変更しようとすると、が失敗 `HRESULT` します。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
**ヘッダー** : CorProf.idl、CorProf.h  
  
**ライブラリ:** CorGuids.lib  
  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のプロファイリング](profiling-enumerations.md)
- [COR_PRF_MONITOR 列挙型](cor-prf-monitor-enumeration.md)
- [ICorProfilerInfo5 インターフェイス](icorprofilerinfo5-interface.md)
