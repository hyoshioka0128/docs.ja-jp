---
title: ICorProfilerCallback::ObjectsAllocatedByClass メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectsAllocatedByClass
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectsAllocatedByClass
helpviewer_keywords:
- ObjectsAllocatedByClass method [.NET Framework profiling]
- ICorProfilerCallback::ObjectsAllocatedByClass method [.NET Framework profiling]
ms.assetid: 91d688f3-a80e-419d-9755-ff94bc04188a
topic_type:
- apiref
ms.openlocfilehash: 7176c0f88daad64f793131aca8c6d9fa592a878c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503277"
---
# <a name="icorprofilercallbackobjectsallocatedbyclass-method"></a>ICorProfilerCallback::ObjectsAllocatedByClass メソッド
最後のガベージコレクション以降に作成された、指定した各クラスのインスタンスの数をプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ObjectsAllocatedByClass(  
    [in] ULONG   cClassCount,  
    [in, size_is(cClassCount)] ClassID classIds[] ,  
    [in, size_is(cClassCount)] ULONG   cObjects[] );  
```  
  
## <a name="parameters"></a>パラメーター  
 `cClassCount`  
 から`classIds`配列と配列のサイズ `cObjects` 。  
  
 `classIds`  
 からクラス Id の配列。各 ID は、1つ以上のインスタンスを持つクラスを指定します。  
  
 `cObjects`  
 から整数の配列。各整数は、配列内の対応するクラスのインスタンスの数を指定し `classIds` ます。  
  
## <a name="remarks"></a>解説  
 `classIds`配列と `cObjects` 配列は並列配列です。 たとえば、 `classIds[i]` とは `cObjects[i]` 同じクラスを参照します。 前のガベージコレクションの後にクラスのインスタンスが作成されていない場合、クラスは省略されます。 `ObjectsAllocatedByClass`コールバックは、大きなオブジェクトヒープに割り当てられたオブジェクトを報告しません。  
  
 によって報告 `ObjectsAllocatedByClass` される数値は、推定値のみです。 正確にカウントするには、 [ICorProfilerCallback:: ObjectAllocated](icorprofilercallback-objectallocated-method.md)を使用します。  
  
 `classIds`対応する配列にアンロード中の型がある場合、配列には1つ以上の null エントリが含まれ `cObjects` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
