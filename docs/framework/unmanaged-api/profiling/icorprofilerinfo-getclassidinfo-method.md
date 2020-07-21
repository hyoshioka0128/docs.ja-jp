---
title: ICorProfilerInfo::GetClassIDInfo メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetClassIDInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetClassIDInfo
helpviewer_keywords:
- GetClassIDInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetClassIDInfo method [.NET Framework profiling]
ms.assetid: 9e93b99e-5aca-415c-8e37-7f33753b612d
topic_type:
- apiref
ms.openlocfilehash: 4fbee938ae86b338f2beb0b48feeee46f144a4a0
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84498493"
---
# <a name="icorprofilerinfogetclassidinfo-method"></a>ICorProfilerInfo::GetClassIDInfo メソッド
指定したクラスの親モジュールとメタデータトークンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetClassIDInfo(  
    [in]  ClassID   classId,  
    [out] ModuleID  *pModuleId,  
    [out] mdTypeDef *pTypeDefToken);  
```  
  
## <a name="parameters"></a>パラメーター  
 `classId`  
 から情報を取得する対象のクラスの ID。  
  
 `pModuleId`  
 入出力クラスの親モジュールの ID へのポインター。  
  
 `pTypeDefToken`  
 入出力クラスのメタデータトークンへのポインター。  
  
## <a name="remarks"></a>解説  
 プロファイラーコードは、 [ICorProfilerInfo:: GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md)を呼び出して、指定されたモジュールのメタデータインターフェイスを取得できます。 `pTypeDefToken` によって参照される場所に返されるメタデータ トークンを使用すると、クラスのメタデータにアクセスできます。  
  
 ジェネリック型の詳細情報を取得するには、 [ICorProfilerInfo2:: GetClassIDInfo2](icorprofilerinfo2-getclassidinfo2-method.md)を使用します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
