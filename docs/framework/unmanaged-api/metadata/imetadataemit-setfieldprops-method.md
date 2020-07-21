---
title: IMetaDataEmit::SetFieldProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetFieldProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetFieldProps
helpviewer_keywords:
- IMetaDataEmit::SetFieldProps method [.NET Framework metadata]
- SetFieldProps method [.NET Framework metadata]
ms.assetid: 47132dda-fa92-4bd1-ae4b-24cd9a60665a
topic_type:
- apiref
ms.openlocfilehash: 220556ec130c7bff7c413405820c4fee0582b051
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008015"
---
# <a name="imetadataemitsetfieldprops-method"></a>IMetaDataEmit::SetFieldProps メソッド
指定したフィールドトークンによって参照されるフィールドの既定値を設定または更新します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetFieldProps (  
    [in]  mdFieldDef  fd,
    [in]  DWORD       dwFieldFlags,
    [in]  DWORD       dwCPlusTypeFlag,
    [in]  void const  *pValue,
    [in]  ULONG       cchValue
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `fd`  
 からターゲットフィールドのトークン。  
  
 `dwFieldFlags`  
 からフィールド属性。 これは、値のビットマスクです `CorFieldAttr` 。  
  
 `dwCPlusTypeFlag`  
 から`ELEMENT_TYPE_` *\** 定数値の。 これは `CorElementType` 値です。 定数が定義されていない場合は、この値をに設定 `ELEMENT_TYPE_END` します。  
  
 `pValue`  
 からフィールドの定数値。  
  
 `cchValue`  
 からのサイズ (Unicode 文字) `pValue` 。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
