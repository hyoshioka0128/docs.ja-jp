---
title: IMetaDataImport::GetPropertyProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetPropertyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetPropertyProps
helpviewer_keywords:
- GetPropertyProps method [.NET Framework metadata]
- IMetaDataImport::GetPropertyProps method [.NET Framework metadata]
ms.assetid: dc0ff3e6-7e7d-4f6c-948d-52b28f5cb78c
topic_type:
- apiref
ms.openlocfilehash: cac5aaa7ed13b6a48b36ad550da8b73d0deb2ee7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491044"
---
# <a name="imetadataimportgetpropertyprops-method"></a>IMetaDataImport::GetPropertyProps メソッド
指定したトークンによって表されるプロパティのメタデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetPropertyProps (  
   [in]  mdProperty        prop,  
   [out] mdTypeDef         *pClass,
   [out] LPCWSTR           szProperty,
   [in]  ULONG             cchProperty,
   [out] ULONG             *pchProperty,
   [out] DWORD             *pdwPropFlags,
   [out] PCCOR_SIGNATURE   *ppvSig,
   [out] ULONG             *pbSig,
   [out] DWORD             *pdwCPlusTypeFlag,
   [out] UVCP_CONSTANT     *ppDefaultValue,  
   [out] ULONG             *pcchDefaultValue,  
   [out] mdMethodDef       *pmdSetter,
   [out] mdMethodDef       *pmdGetter,
   [out] mdMethodDef       rmdOtherMethod[],  
   [in]  ULONG             cMax,
   [out] ULONG             *pcOtherMethod
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `prop`  
 からメタデータを返すプロパティを表すトークン。  
  
 `pClass`  
 入出力プロパティを実装する型を表す TypeDef トークンへのポインター。  
  
 `szProperty`  
 入出力プロパティ名を保持するバッファー。  
  
 `cchProperty`  
 からのワイド文字のサイズ `szProperty` 。  
  
 `pchProperty`  
 入出力で返されたワイド文字の数 `szProperty` 。  
  
 `pdwPropFlags`  
 入出力プロパティに適用されている属性フラグへのポインター。 この値は、 [Corpropertyattr](corpropertyattr-enumeration.md)列挙子のビットマスクです。  
  
 `ppvSig`  
 入出力プロパティのメタデータシグネチャへのポインター。  
  
 `pbSig`  
 入出力で返されたバイト数 `ppvSig` 。  
  
 `pdwCPlusTypeFlag`  
 入出力プロパティの既定値である定数の型を指定するフラグ。 この値は CorElementType 列挙子からのものです。  
  
 `ppDefaultValue`  
 入出力このプロパティの既定値を格納するバイトへのポインター。  
  
 `pcchDefaultValue`  
 入出力が ELEMENT_TYPE_STRING の場合は、のワイド文字のサイズ `ppDefaultValue` `pdwCPlusTypeFlag` 。それ以外の場合、この値は関係ありません。 この場合、の長さは、 `ppDefaultValue` によって指定された型から推論され `pdwCPlusTypeFlag` ます。  
  
 `pmdSetter`  
 入出力プロパティの set アクセサーメソッドを表す MethodDef トークンへのポインター。  
  
 `pmdGetter`  
 入出力プロパティの get アクセサーメソッドを表す MethodDef トークンへのポインター。  
  
 `rmdOtherMethod`  
 入出力プロパティに関連付けられている他のメソッドを表す MethodDef トークンの配列。  
  
 `cMax`  
 [in] `rmdOtherMethod` 配列の最大サイズ。 すべてのメソッドを保持するのに十分な大きさの配列を指定しなかった場合、警告なしにスキップされます。  
  
 `pcOtherMethod`  
 入出力で返される MethodDef トークンの数 `rmdOtherMethod` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
