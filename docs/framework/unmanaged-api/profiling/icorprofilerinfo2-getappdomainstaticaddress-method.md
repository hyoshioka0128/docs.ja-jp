---
title: ICorProfilerInfo2::GetAppDomainStaticAddress メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetAppDomainStaticAddress
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetAppDomainStaticAddress
helpviewer_keywords:
- ICorProfilerInfo2::GetAppDomainStaticAddress method [.NET Framework profiling]
- GetAppDomainStaticAddress method [.NET Framework profiling]
ms.assetid: 2a9e0ea7-a9e2-4817-b1c4-fcf15b215ea9
topic_type:
- apiref
ms.openlocfilehash: 3dc5f04504cca632892c16d31c92a33935b356e0
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497336"
---
# <a name="icorprofilerinfo2getappdomainstaticaddress-method"></a>ICorProfilerInfo2::GetAppDomainStaticAddress メソッド
指定したアプリケーションドメインのスコープ内にある、指定したアプリケーションドメインの静的フィールドのアドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
RESULT GetAppDomainStaticAddress(  
    [in] ClassID classId,  
    [in] mdFieldDef fieldToken,  
    [in] AppDomainID appDomainId,  
    [out] void **ppAddress);  
```  
  
## <a name="parameters"></a>パラメーター  
 `classId`  
 から要求されたアプリケーションドメインの静的フィールドを含むクラスのクラス ID。  
  
 `fieldToken`  
 から要求されたアプリケーションドメインの静的フィールドのメタデータトークン。  
  
 `appDomainId`  
 から要求された静的フィールドのスコープであるアプリケーションドメインの ID。  
  
 `ppAddress`  
 入出力指定されたアプリケーションドメイン内の静的フィールドのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 `GetAppDomainStaticAddress`メソッドは、次のいずれかを返す場合があります。  
  
- 指定されたコンテキストで、指定された静的フィールドにアドレスが割り当てられていない場合は CORPROF_E_DATAINCOMPLETE HRESULT。  
  
- ガベージコレクションヒープ内に存在する可能性があるオブジェクトのアドレス。 これらのアドレスは、ガベージコレクションの後に無効になることがあります。そのため、ガベージコレクションの後、プロファイラーはそれらが有効であると想定してはなりません。  
  
 では、クラスのクラスコンストラクターが完了する前に、 `GetAppDomainStaticAddress` すべての静的フィールドに対して CORPROF_E_DATAINCOMPLETE が返されます。ただし、静的フィールドの一部は既に初期化されており、ガベージコレクションオブジェクトがルート化される場合があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
