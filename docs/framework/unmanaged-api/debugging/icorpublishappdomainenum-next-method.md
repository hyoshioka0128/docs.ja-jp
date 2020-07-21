---
title: ICorPublishAppDomainEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorPublishAppDomainEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishAppDomainEnum::Next
helpviewer_keywords:
- Next method, ICorPublishAppDomainEnum interface [.NET Framework debugging]
- ICorPublishAppDomainEnum::Next method [.NET Framework debugging]
ms.assetid: ad37cd10-0339-4d08-9b0e-4b3428bb4dc3
topic_type:
- apiref
ms.openlocfilehash: c5ac38005410ae6ed9c2f4160e926987791ad604
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421216"
---
# <a name="icorpublishappdomainenumnext-method"></a>ICorPublishAppDomainEnum::Next メソッド
現在プロセスに存在する、指定した数のアプリケーションドメインを、現在の位置から取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next (  
    [in] ULONG  celt,  
    [out, size_is(celt), length_is(*pceltFetched)]
        ICorPublishAppDomain **objects,  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 から取得する要素の数。  
  
 `objects`  
 入出力取得された[ICorPublishAppDomain](icorpublishappdomain-interface.md)オブジェクトの配列へのポインター。各オブジェクトは、アプリケーションドメインを表します。  
  
 `pceltFetched`  
 入出力実際に返されたアプリケーションドメインの数へのポインター。 が1の場合、この値は null `celt` になります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorPublishAppDomainEnum インターフェイス](icorpublishappdomainenum-interface.md)
