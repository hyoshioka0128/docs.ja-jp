---
title: IMetaDataEmit::DefineProperty メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineProperty
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineProperty
helpviewer_keywords:
- IMetaDataEmit::DefineProperty method [.NET Framework metadata]
- DefineProperty method [.NET Framework metadata]
ms.assetid: 5c4c1dc2-d40d-4173-bbe6-7058fb21c98f
topic_type:
- apiref
ms.openlocfilehash: 479cb25ad8e1c263d3539a4203ac5bea781eb931
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009380"
---
# <a name="imetadataemitdefineproperty-method"></a>IMetaDataEmit::DefineProperty メソッド
指定したアクセサーとメソッドアクセサーを使用して、指定した型のプロパティ定義を作成 `get` `set` し、そのプロパティ定義へのトークンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineProperty (
    [in]  mdTypeDef          td,
    [in]  LPCWSTR            szProperty,
    [in]  DWORD              dwPropFlags,
    [in]  PCCOR_SIGNATURE    pvSig,
    [in]  ULONG              cbSig,
    [in]  DWORD              dwCPlusTypeFlag,
    [in]  void const         *pValue,
    [in]  ULONG              cchValue,
    [in]  mdMethodDef        mdSetter,
    [in]  mdMethodDef        mdGetter,
    [in]  mdMethodDef        rmdOtherMethods[],
    [out] mdProperty         *pmdProp
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `td`  
 からプロパティが定義されているクラスまたはインターフェイスのトークン。  
  
 `szProperty`  
 からプロパティの名前。  
  
 `dwPropFlags`  
 からプロパティフラグ。  
  
 `pvSig`  
 からプロパティシグネチャ。  
  
 `cbSig`  
 からのバイト数 `pvSig` 。  
  
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
 からプロパティに関連付けられている他のメソッドの配列。 を使用して配列を終了 `mdTokenNil` します。  
  
 `pmdProp`  
 入出力`mdProperty`割り当てられたトークン。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
