---
title: ICorProfilerInfo::GetTokenAndMetadataFromFunction メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetTokenAndMetadataFromFunction
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetTokenAndMetadataFromFunction
helpviewer_keywords:
- ICorProfilerInfo::GetTokenAndMetadataFromFunction method [.NET Framework profiling]
- GetTokenAndMetadataFromFunction method [.NET Framework profiling]
ms.assetid: e525aa16-c923-4b16-833b-36f1f0dd70fc
topic_type:
- apiref
ms.openlocfilehash: 1cc05f4c10f4a5b042ff14c05f3c85a7b5935184
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497895"
---
# <a name="icorprofilerinfogettokenandmetadatafromfunction-method"></a>ICorProfilerInfo::GetTokenAndMetadataFromFunction メソッド
指定された関数のトークンに対して使用できるメタデータトークンとメタデータインターフェイスインスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTokenAndMetaDataFromFunction(  
    [in]  FunctionID functionId,  
    [in]  REFIID     riid,  
    [out] IUnknown   **ppImport,  
    [out] mdToken    *pToken);  
```  
  
## <a name="parameters"></a>パラメーター  
 `functionId`  
 からメタデータトークンとメタデータインターフェイスを取得する対象の関数の ID。  
  
 `riid`  
 からインスタンスを取得するメタデータインターフェイスの参照 ID。  
  
 `ppImport`  
 入出力指定された関数のトークンに対して使用できるメタデータインターフェイスインスタンスのアドレスへのポインター。  
  
 `pToken`  
 入出力指定された関数のメタデータトークンへのポインター。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
