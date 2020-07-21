---
title: ICorPublishEnum::Clone メソッド
ms.date: 03/30/2017
api_name:
- ICorPublishEnum.Clone
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishEnum::Clone
helpviewer_keywords:
- Clone method, ICorPublishEnum interface [.NET Framework debugging]
- ICorPublishEnum::Clone method [.NET Framework debugging]
ms.assetid: c9a26ea3-b8eb-4b8e-854f-9a2ca26b3b39
topic_type:
- apiref
ms.openlocfilehash: 38f49e8fe632e9b38ede8815de6d8865278351f9
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421203"
---
# <a name="icorpublishenumclone-method"></a>ICorPublishEnum::Clone メソッド
この[ICorPublishEnum](icorpublishenum-interface.md)オブジェクトのコピーを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Clone (  
    [out] ICorPublishEnum   **ppEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力`ICorPublishEnum`このオブジェクトのコピーであるオブジェクトのアドレスへのポインター `ICorPublishEnum` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorPub .idl、CorPub .h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorPublishEnum インターフェイス](icorpublishenum-interface.md)
