---
title: IMetaDataImport::GetTypeDefProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetTypeDefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetTypeDefProps
helpviewer_keywords:
- GetTypeDefProps method [.NET Framework metadata]
- IMetaDataImport::GetTypeDefProps method [.NET Framework metadata]
ms.assetid: 00061a25-ba05-47a7-b984-fd916b06b149
topic_type:
- apiref
ms.openlocfilehash: 6346b1e34e508e5c173bfd0119ac7451d7eef40e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490797"
---
# <a name="imetadataimportgettypedefprops-method"></a>IMetaDataImport::GetTypeDefProps メソッド
<xref:System.Type>指定した TypeDef トークンによって表されるのメタデータ情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTypeDefProps (  
   [in]  mdTypeDef   td,  
   [out] LPWSTR      szTypeDef,  
   [in]  ULONG       cchTypeDef,  
   [out] ULONG       *pchTypeDef,  
   [out] DWORD       *pdwTypeDefFlags,  
   [out] mdToken     *ptkExtends  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `td`  
 からメタデータを返す型を表す TypeDef トークン。  
  
 `szTypeDef`  
 入出力型名を格納しているバッファー。  
  
 `cchTypeDef`  
 からのワイド文字のサイズ `szTypeDef` 。  
  
 `pchTypeDef`  
 入出力で返されたワイド文字の数 `szTypeDef` 。  
  
 `pdwTypeDefFlags`  
 入出力型定義を変更するすべてのフラグへのポインター。 この値は、 [Cortypeattr](cortypeattr-enumeration.md)列挙子のビットマスクです。  
  
 `ptkExtends`  
 入出力要求された型の基本型を表す TypeDef または TypeRef メタデータトークン。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
