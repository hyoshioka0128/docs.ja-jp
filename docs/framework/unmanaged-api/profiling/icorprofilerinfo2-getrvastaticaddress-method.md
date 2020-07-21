---
title: ICorProfilerInfo2::GetRVAStaticAddress メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetRVAStaticAddress
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetRVAStaticAddress
helpviewer_keywords:
- GetRVAStaticAddress method [.NET Framework profiling]
- ICorProfilerInfo2::GetRVAStaticAddress method [.NET Framework profiling]
ms.assetid: a25a8f8b-5cfa-440d-9376-a1a1c3a9fc11
topic_type:
- apiref
ms.openlocfilehash: 525fa2efa39909390d874fb97d9f11e647340ea9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496946"
---
# <a name="icorprofilerinfo2getrvastaticaddress-method"></a>ICorProfilerInfo2::GetRVAStaticAddress メソッド
指定した相対仮想アドレス (RVA) の静的フィールドのアドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRVAStaticAddress(  
    [in] ClassID classId,  
    [in] mdFieldDef fieldToken,  
    [out] void **ppAddress);  
```  
  
## <a name="parameters"></a>パラメーター  
 `classId`  
 から要求された RVA 静的フィールドを含むクラスの ID。  
  
 `fieldToken`  
 から要求された RVA 静的フィールドのメタデータトークン。  
  
 `ppAddress`  
 入出力RVA の静的フィールドのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 `GetRVAStaticAddress`メソッドは、次のいずれかを返す場合があります。  
  
- 指定されたコンテキストで、指定された静的フィールドにアドレスが割り当てられていない場合は CORPROF_E_DATAINCOMPLETE HRESULT。  
  
- ガベージコレクションヒープ内に存在する可能性があるオブジェクトのアドレス。 これらのアドレスは、ガベージコレクションの後に無効になることがあります。そのため、ガベージコレクションの後、プロファイラーはそれらが有効であると想定してはなりません。  
  
 では、クラスのクラスコンストラクターが完了する前に、 `GetRVAStaticAddress` すべての静的フィールドに対して CORPROF_E_DATAINCOMPLETE が返されます。ただし、一部の静的フィールドは既に初期化されており、ガベージコレクションオブジェクトをルート化する場合があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
