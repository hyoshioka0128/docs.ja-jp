---
title: ICorPublishAppDomain::GetID メソッド
ms.date: 03/30/2017
api_name:
- ICorPublishAppDomain.GetID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishAppDomain::GetID
helpviewer_keywords:
- GetID method, ICorPublishAppDomain interface [.NET Framework debugging]
- ICorPublishAppDomain::GetID method [.NET Framework debugging]
ms.assetid: 229437e3-1465-4bd8-8846-9804b2488133
topic_type:
- apiref
ms.openlocfilehash: 36c5c674f3cdf867107b9ee85a5befadc9246d78
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396306"
---
# <a name="icorpublishappdomaingetid-method"></a>ICorPublishAppDomain::GetID メソッド
この[ICorPublishAppDomain](icorpublishappdomain-interface.md)の一意の識別子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetID (  
    [out] ULONG32   *puId  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `puId`  
 入出力アプリケーションドメインの識別子へのポインター。  
  
## <a name="remarks"></a>解説  
 識別子は、含んでいるプロセスのスコープ内でのみ一意です。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorPublishAppDomain インターフェイス](icorpublishappdomain-interface.md)
