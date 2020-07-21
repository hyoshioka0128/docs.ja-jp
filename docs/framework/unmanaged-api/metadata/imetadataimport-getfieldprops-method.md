---
title: IMetaDataImport::GetFieldProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetFieldProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetFieldProps
helpviewer_keywords:
- IMetaDataImport::GetFieldProps method [.NET Framework metadata]
- GetFieldProps method [.NET Framework metadata]
ms.assetid: 7b0e9b10-8cef-4ba6-8432-40bf63e65ab1
topic_type:
- apiref
ms.openlocfilehash: 2bd05b49c3d51ac13865997910c99cc0cd5ca2d9
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491247"
---
# <a name="imetadataimportgetfieldprops-method"></a>IMetaDataImport::GetFieldProps メソッド
指定した FieldDef トークンによって参照されるフィールドに関連付けられているメタデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFieldProps (  
   [in]  mdFieldDef        mb,
   [out] mdTypeDef         *pClass,  
   [out] LPWSTR            szField,  
   [in]  ULONG             cchField,
   [out] ULONG             *pchField,  
   [out] DWORD             *pdwAttr,  
   [in]  PCCOR_SIGNATURE   *ppvSigBlob,
   [out] ULONG             *pcbSigBlob,
   [out] DWORD             *pdwCPlusTypeFlag,
   [out] UVCP_CONSTANT     *ppValue,  
   [out] ULONG             *pcchValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mb`  
 から関連付けられたメタデータを取得する対象のフィールドを表す FieldDef トークン。  
  
 `pClass`  
 入出力フィールドが属するクラスの型を表す TypeDef トークンへのポインター。  
  
 `szField`  
 入出力フィールドの名前。  
  
 `cchField`  
 から*Szfield*のバッファーのサイズ (ワイド文字単位)。  
  
 `pchField`  
 入出力返されたバッファーの実際のサイズ。  
  
 `pdwAttr`  
 入出力フィールドのメタデータに関連付けられているフラグ。  
  
 `ppvSigBlob`  
 からフィールドを説明するバイナリメタデータ値へのポインター。  
  
 `pcbSigBlob`  
 入出力のサイズ (バイト単位) `ppvSigBlob` 。  
  
 `pdwCPlusTypeFlag`  
 入出力フィールドの値の型を指定するフラグ。  
  
 `ppValue`  
 入出力フィールドの定数値。  
  
 `pcchValue`  
 入出力の文字数のサイズ `ppValue` 。文字列が存在しない場合は0。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
