---
title: IMetaDataEmit::SetPropertyProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetPropertyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetPropertyProps
helpviewer_keywords:
- SetPropertyProps method [.NET Framework metadata]
- IMetaDataEmit::SetPropertyProps method [.NET Framework metadata]
ms.assetid: e2501fc8-b2bc-4dcc-9205-e3acd5a53ffe
topic_type:
- apiref
ms.openlocfilehash: b5af877c26c20bf64a27618bf24a7bce5b410419
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007781"
---
# <a name="imetadataemitsetpropertyprops-method"></a>IMetaDataEmit::SetPropertyProps メソッド
以前の呼び出し[プロパティメソッド](imetadataemit-defineproperty-method.md)の呼び出しで定義されたプロパティのメタデータに格納されている機能を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetPropertyProps (
    [in]  mdProperty      pr,
    [in]  DWORD           dwPropFlags,
    [in]  DWORD           dwCPlusTypeFlag,
    [in]  void const      *pValue,
    [in]  ULONG           cchValue,
    [in]  mdMethodDef     mdSetter,
    [in]  mdMethodDef     mdGetter,
    [in]  mdMethodDef     rmdOtherMethods[]
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pr`  
 から変更するプロパティのトークン  
  
 `dwPropFlags`  
 からプロパティフラグ。  
  
 `dwCPlusTypeFlag`  
 からプロパティの既定値の型。  
  
 `pValue`  
 からプロパティの既定値。  
  
 `cchValue`  
 から内の (Unicode) 文字の数 `pValue` 。  
  
 `mdSetter`  
 からプロパティ値を設定するメソッド。  
  
 `mdGetter`  
 からプロパティ値を取得するメソッド。  
  
 `rmdOtherMethods[]`  
 からプロパティに関連付けられている他のメソッドの配列。 トークンを使用して、この配列を終了 `mdTokenNil` します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
