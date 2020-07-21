---
title: IMetaDataEmit::SetParamProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetParamProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetParamProps
helpviewer_keywords:
- IMetaDataEmit::SetParamProps method [.NET Framework metadata]
- SetParamProps method [.NET Framework metadata]
ms.assetid: a95a3908-9f87-4084-937e-8e01ef03ad63
topic_type:
- apiref
ms.openlocfilehash: b710f966f519e2702607b7e186fff5986110d391
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007820"
---
# <a name="imetadataemitsetparamprops-method"></a>IMetaDataEmit::SetParamProps メソッド
[IMetaDataEmit::D efineParam](imetadataemit-defineparam-method.md)の前の呼び出しで定義されたメソッドパラメーターの機能を設定または変更します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetParamProps (
    [in]  mdParamDef  pd,
    [in]  LPCWSTR     szName,
    [in]  DWORD       dwParamFlags,
    [in]  DWORD       dwCPlusTypeFlag,
    [in]  void const  *pValue,
    [in]  ULONG       cchValue
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pd`  
 から対象のパラメーターのトークン。  
  
 `szName`  
 からUnicode でのパラメーターの名前。  
  
 `dwParamFlags`  
 からパラメーターのフラグ。  
  
 `dwCPlusTypeFlag`  
 から定数値の ELEMENT_TYPE_ *。  
  
 `pValue`  
 からパラメーターの定数値。  
  
 `cchValue`  
 からの (Unicode) 文字のサイズ `pValue` 。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
