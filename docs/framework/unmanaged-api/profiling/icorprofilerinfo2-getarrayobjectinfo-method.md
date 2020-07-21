---
title: ICorProfilerInfo2::GetArrayObjectInfo メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetArrayObjectInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetArrayObjectInfo
helpviewer_keywords:
- ICorProfilerInfo2::GetArrayObjectInfo method [.NET Framework profiling]
- GetArrayObjectInfo method [.NET Framework profiling]
ms.assetid: bda75017-739f-4ce5-9000-f3b526e8473c
topic_type:
- apiref
ms.openlocfilehash: 368b8f270797beb525e0745a29990667913f4071
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497360"
---
# <a name="icorprofilerinfo2getarrayobjectinfo-method"></a>ICorProfilerInfo2::GetArrayObjectInfo メソッド
配列オブジェクトに関する詳細情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetArrayObjectInfo(  
    [in] ObjectID objectId,  
    [in] ULONG32 cDimensions,  
    [out, size_is(cDimensions), length_is(cDimensions)] ULONG32 pDimensionSizes[],  
    [out, size_is(cDimensions), length_is(cDimensions)] int pDimensionLowerBounds[],  
    [out] BYTE **ppData);  
```  
  
## <a name="parameters"></a>パラメーター  
 `objectId`  
 から有効な配列オブジェクトの ID。  
  
 `cDimensions`  
 から配列のランク (次元数)。  
  
 `pDimensionSizes`  
 入出力それぞれが配列の次元のサイズを表す整数を格納している配列。  
  
 `pDimensionLowerBounds`  
 入出力それぞれが配列の次元の下限を表す整数を格納している配列。  
  
 `ppData`  
 入出力配列の生バッファーのアドレスへのポインター。これは、C++ 規則に従ってレイアウトされます。  
  
## <a name="remarks"></a>解説  
 `pDimensionSizes`とは `pDimensionLowerBounds` 並列配列であるため、各配列内の同じインデックスにある要素は同じエンティティの特性です。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
