---
title: ICorProfilerInfo2::GetContextStaticAddress メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetContextStaticAddress
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetContextStaticAddress
helpviewer_keywords:
- GetContextStaticAddress method [.NET Framework profiling]
- ICorProfilerInfo2::GetContextStaticAddress method [.NET Framework profiling]
ms.assetid: 2b374116-0972-416a-8cf5-79213129be9a
topic_type:
- apiref
ms.openlocfilehash: 7550caaa7cb4d7ed77dc36ecf0ce0e0cbc541db7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497063"
---
# <a name="icorprofilerinfo2getcontextstaticaddress-method"></a>ICorProfilerInfo2::GetContextStaticAddress メソッド
指定されたコンテキストのスコープ内にある、指定されたコンテキスト静的フィールドのアドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetContextStaticAddress(  
    [in] ClassID classId,  
    [in] mdFieldDef fieldToken,  
    [in] ContextID contextId,  
    [out] void **ppAddress);  
```  
  
## <a name="parameters"></a>パラメーター  
 `classId`  
 から要求されたコンテキスト静的フィールドを含むクラスの ID。  
  
 `fieldToken`  
 から要求されたコンテキスト静的フィールドのメタデータトークン。  
  
 `contextId`  
 から要求されたコンテキスト静的フィールドのスコープであるコンテキストの ID。  
  
 `ppAddress`  
 入出力指定されたコンテキスト内の静的フィールドのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 `GetContextStaticAddress`メソッドは、次のいずれかを返す場合があります。  
  
- 指定されたコンテキストで、指定された静的フィールドにアドレスが割り当てられていない場合は CORPROF_E_DATAINCOMPLETE HRESULT。  
  
- ガベージコレクションヒープ内に存在する可能性があるオブジェクトのアドレス。 これらのアドレスは、ガベージコレクションの後に無効になることがあります。そのため、ガベージコレクションの後、プロファイラーはそれらが有効であると想定してはなりません。  
  
 では、クラスのクラスコンストラクターが完了する前に、 `GetContextStaticAddress` すべての静的フィールドに対して CORPROF_E_DATAINCOMPLETE が返されます。ただし、静的フィールドの一部は既に初期化されており、ガベージコレクションオブジェクトがルート化される場合があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
