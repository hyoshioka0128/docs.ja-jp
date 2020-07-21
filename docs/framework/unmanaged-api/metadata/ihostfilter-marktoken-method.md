---
title: IHostFilter::MarkToken メソッド
ms.date: 03/30/2017
api_name:
- IHostFilter.MarkToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostFilter::MarkToken
helpviewer_keywords:
- MarkToken method, IHostFilter interface [.NET Framework metadata]
- IHostFilter::MarkToken method [.NET Framework metadata]
ms.assetid: d7061343-d0a3-4fd5-b312-61974f98bd62
topic_type:
- apiref
ms.openlocfilehash: 11529ce896f265f2b200fa6e511d4b913e9147c8
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008223"
---
# <a name="ihostfiltermarktoken-method"></a>IHostFilter::MarkToken メソッド
指定されたメタデータトークンが処理されることを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT MarkToken (  
    [in]  mdToken         tk  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tk`  
 から処理するメタデータトークン。  
  
## <a name="remarks"></a>コメント  
 通常、トークンがメタデータスコープ内にある場合は、トークンを処理する必要があります。 メソッドは、 `MarkToken` [IMetaDataEmit:: SetHandler](imetadataemit-sethandler-method.md)メソッドを使用してメタデータエンジンに渡されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ インターフェイス](metadata-interfaces.md)
- [IHostFilter インターフェイス](ihostfilter-interface.md)
