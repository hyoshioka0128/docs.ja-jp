---
title: ICorProfilerInfo2::GetStaticFieldInfo メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetStaticFieldInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetStaticFieldInfo
helpviewer_keywords:
- ICorProfilerInfo2::GetStaticFieldInfo method [.NET Framework profiling]
- GetStaticFieldInfo method [.NET Framework profiling]
ms.assetid: fc663e76-e23f-49a8-bdd5-52cdf1a3b2b3
topic_type:
- apiref
ms.openlocfilehash: e1dd6addd9053ffb6cf2ce23408673d8fca17cb5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496842"
---
# <a name="icorprofilerinfo2getstaticfieldinfo-method"></a>ICorProfilerInfo2::GetStaticFieldInfo メソッド
指定したフィールドに適用される静的の種類を示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetStaticFieldInfo (  
    [in] ClassID               classId,  
    [in] mdFieldDef            fieldToken,  
    [out] COR_PRF_STATIC_TYPE  *pFieldInfo);  
```  
  
## <a name="parameters"></a>パラメーター  
 `classId`  
 から静的フィールドが定義されているクラスの ID。  
  
 `fieldToken`  
 から静的フィールドのメタデータトークン。  
  
 `pFieldInfo`  
 入出力指定されたフィールドが静的かどうかを示す[COR_PRF_STATIC_TYPE](cor-prf-static-type-enumeration.md)列挙体の値へのポインター。存在する場合は、フィールドに適用される静的の種類。  
  
## <a name="remarks"></a>解説  
 この情報は、静的フィールドのアドレスを取得するために呼び出す関数を決定するために使用できます。  
  
 プロファイラーコードでは、静的フィールドのメタデータを確認して、実際にアドレスがあることを確認する必要があります。 静的リテラル (つまり、定数) はメタデータにのみ存在し、アドレスを持ちません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
