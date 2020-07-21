---
title: IMetaDataImport2::EnumMethodSpecs メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.EnumMethodSpecs
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::EnumMethodSpecs
helpviewer_keywords:
- IMetaDataImport2::EnumMethodSpecs method [.NET Framework metadata]
- EnumMethodSpecs method [.NET Framework metadata]
ms.assetid: b3fc1e6c-bcb6-4915-baf8-7dc0a31b8724
topic_type:
- apiref
ms.openlocfilehash: 8f6fbc570e7ea85aca5b365611d58a1700fb27cd
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490719"
---
# <a name="imetadataimport2enummethodspecs-method"></a>IMetaDataImport2::EnumMethodSpecs メソッド
指定した MethodDef または MemberRef トークンに関連付けられている MethodSpec トークンの配列の列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumMethodSpecs (  
    [in, out] HCORENUM      *phEnum,
    [in]      mdToken       tk,  
    [out]     mdMethodSpec  rMethodSpecs[],  
    [in]      ULONG         cMax,  
    [out]     ULONG         *pcMethodSpecs  
);
```  
  
## <a name="parameters"></a>パラメーター  
 `phEnum`  
 [入力、出力]の列挙子へのポインター `rMethodSpecs` 。  
  
 `tk`  
 からMethodSpec トークンを列挙するメソッドを表す MemberRef または MethodDef トークン。 の値 `tk` が 0 (ゼロ) の場合、スコープ内のすべての MethodSpec トークンが列挙されます。  
  
 `rMethodSpecs`  
 入出力列挙する MethodSpec トークンの配列。  
  
 `cMax`  
 からに格納するトークンの要求された最大数 `rMethodSpecs` 。  
  
 `pcMethodSpecs`  
 入出力に格納された、返されたトークンの数 `rMethodSpecs` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|`S_OK`|`EnumMethodSpecs`正常に返されました。|  
|`S_FALSE`|`phEnum`にメンバー要素がありません。 この場合、 `pcMethodSpecs` は 0 (ゼロ) に設定されます。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
