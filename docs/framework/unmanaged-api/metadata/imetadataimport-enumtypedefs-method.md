---
title: IMetaDataImport::EnumTypeDefs メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumTypeDefs
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumTypeDefs
helpviewer_keywords:
- EnumTypeDefs method [.NET Framework metadata]
- IMetaDataImport::EnumTypeDefs method [.NET Framework metadata]
ms.assetid: 4e508711-da92-4381-aaf8-6803075cdaa2
topic_type:
- apiref
ms.openlocfilehash: cdfd4e10236d546af2555b125d44233172849a21
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503732"
---
# <a name="imetadataimportenumtypedefs-method"></a>IMetaDataImport::EnumTypeDefs メソッド
現在のスコープ内のすべての型を表す TypeDef トークンを列挙します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumTypeDefs (  
   [out] HCORENUM   *phEnum,
   [in]  mdTypeDef  rTypeDefs[],  
   [in]  ULONG      cMax,
   [out] ULONG      *pcTypeDefs  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `phEnum`  
 入出力新しい列挙子へのポインター。 このメソッドの最初の呼び出しでは、この値は NULL である必要があります。  
  
 `rTypeDefs`  
 からTypeDef トークンを格納するために使用される配列。  
  
 `cMax`  
 [in] `rTypeDefs` 配列の最大サイズ。  
  
 `pcTypeDefs`  
 入出力で返された TypeDef トークンの数 `rTypeDefs` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|`S_OK`|`EnumTypeDefs`正常に返されました。|  
|`S_FALSE`|列挙するトークンがありません。 この場合、 `pcTypeDefs` は0になります。|  
  
## <a name="remarks"></a>解説  
 TypeDef トークンは、クラスやインターフェイスなどの型、および拡張メカニズムを使用して追加された型を表します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
