---
title: IMetaDataImport2::GetGenericParamConstraintProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.GetGenericParamConstraintProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::GetGenericParamConstraintProps
helpviewer_keywords:
- IMetaDataImport2::GetGenericParamConstraintProps method [.NET Framework metadata]
- GetGenericParamConstraintProps method [.NET Framework metadata]
ms.assetid: c5fee4a0-b132-4e5e-8730-e586ce314b9a
topic_type:
- apiref
ms.openlocfilehash: 8a1cdff313dae73e3f5e8918ff2ef395c80b115d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490628"
---
# <a name="imetadataimport2getgenericparamconstraintprops-method"></a>IMetaDataImport2::GetGenericParamConstraintProps メソッド
指定された制約トークンによって表されるジェネリックパラメーター制約に関連付けられているメタデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetGenericParamConstraintProps (  
   [in]  mdGenericParamConstraint  gpc,  
   [out] mdGenericParam            *ptGenericParam,  
   [out] mdToken                   *ptkConstraintType  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `gpc`  
 からメタデータを返す対象のジェネリックパラメーター制約へのトークン。  
  
 `ptGenericParam`  
 入出力制約されているジェネリックパラメーターを表すトークンへのポインター。  
  
 `ptkConstraintType`  
 入出力の制約を表す TypeDef、TypeRef、または TypeSpec トークンへのポインター `ptGenericParam` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
