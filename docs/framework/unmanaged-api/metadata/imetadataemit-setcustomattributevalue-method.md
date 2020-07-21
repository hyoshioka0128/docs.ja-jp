---
title: IMetaDataEmit::SetCustomAttributeValue メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetCustomAttributeValue
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetCustomAttributeValue
helpviewer_keywords:
- SetCustomAttributeValue method [.NET Framework metadata]
- IMetaDataEmit::SetCustomAttributeValue method [.NET Framework metadata]
ms.assetid: f721c863-9642-4e64-917a-65f9e55c25b9
topic_type:
- apiref
ms.openlocfilehash: 6e24db7da7abbdb597b8ff64515e8053667af3ff
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008769"
---
# <a name="imetadataemitsetcustomattributevalue-method"></a>IMetaDataEmit::SetCustomAttributeValue メソッド
[IMetaDataEmit::D efinecustomattribute](imetadataemit-definecustomattribute-method.md)の前の呼び出しで定義されたカスタム属性の値を設定または更新します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetCustomAttributeValue (
    [in]  mdCustomAttribute       pcv,
    [in]  void const              *pCustomAttribute,
    [in]  ULONG                   cbCustomAttribute
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pcv`  
 から対象のカスタム属性のトークン。  
  
 `pCustomAttribute`  
 からカスタム属性を格納している配列へのポインター。  
  
 `cbCustomAttribute`  
 からカスタム属性のサイズ (バイト単位)。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
