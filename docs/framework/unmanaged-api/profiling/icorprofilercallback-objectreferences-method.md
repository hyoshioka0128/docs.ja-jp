---
title: ICorProfilerCallback::ObjectReferences メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectReferences
helpviewer_keywords:
- ObjectReferences method [.NET Framework profiling]
- ICorProfilerCallback::ObjectReferences method [.NET Framework profiling]
ms.assetid: dd5e9b64-b4a3-4ba6-9be6-ddb540f4ffcf
topic_type:
- apiref
ms.openlocfilehash: 12a0792e8fafc73b480de6bacc86f98470dfedf7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503290"
---
# <a name="icorprofilercallbackobjectreferences-method"></a>ICorProfilerCallback::ObjectReferences メソッド
指定したオブジェクトによって参照されているメモリ内のオブジェクトに関する情報をプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ObjectReferences(  
    [in]  ObjectID objectId,  
    [in]  ClassID  classId,  
    [in]  ULONG    cObjectRefs,  
    [in, size_is(cObjectRefs)] ObjectID objectRefIds[] );  
```  
  
## <a name="parameters"></a>パラメーター  
 `objectId`  
 からオブジェクトを参照しているオブジェクトの ID。  
  
 `classId`  
 から指定したオブジェクトがインスタンスであるクラスの ID。  
  
 `cObjectRefs`  
 から指定したオブジェクトによって参照されるオブジェクトの数 (つまり、配列内の要素の数 `objectRefIds` )。  
  
 `objectRefIds`  
 からによって参照されているオブジェクトの Id の配列 `objectId` 。  
  
## <a name="remarks"></a>解説  
 `ObjectReferences`メソッドは、ガベージコレクションが完了した後にヒープ内の残りのオブジェクトに対して呼び出されます。 プロファイラーがこのコールバックからエラーを返すと、プロファイリングサービスは、次のガベージコレクションまでこのコールバックの呼び出しを中止します。  
  
 コールバックは、 `ObjectReferences` [ICorProfilerCallback:: rootreferences](icorprofilercallback-rootreferences-method.md)コールバックと共に使用して、ランタイムの完全なオブジェクト参照グラフを作成できます。 共通言語ランタイム (CLR) では、各オブジェクト参照がメソッドによって1回だけ報告され `ObjectReferences` ます。  
  
 によって返されるオブジェクト Id `ObjectReferences` は、オブジェクトの移動中にガベージコレクションが発生する可能性があるため、コールバック自体では無効です。 そのため、呼び出し中にプロファイラーがオブジェクトの検査を試行することはできません `ObjectReferences` 。 [ICorProfilerCallback2:: GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)が呼び出されると、ガベージコレクションが完了し、検査を安全に行うことができます。  
  
 Null は、が `ClassId` `objectId` アンロード中の型を持つことを示します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
