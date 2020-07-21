---
title: IMetaDataImport2::GetGenericParamProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.GetGenericParamProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::GetGenericParamProps
helpviewer_keywords:
- IMetaDataImport2::GetGenericParamProps method [.NET Framework metadata]
- GetGenericParamProps method [.NET Framework metadata]
ms.assetid: dbb21e67-712b-49e7-a27c-a1e73ffd46c5
topic_type:
- apiref
ms.openlocfilehash: 7e97b2d4ad1fec4675d1484959b115a4d4b87e90
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490615"
---
# <a name="imetadataimport2getgenericparamprops-method"></a>IMetaDataImport2::GetGenericParamProps メソッド
指定したトークンによって表されるジェネリックパラメーターに関連付けられているメタデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetGenericParamProps (  
   [in]  mdGenericParam  gp,  
   [out] ULONG           *pulParamSeq,  
   [out] DWORD           *pdwParamFlags,  
   [out] mdToken         *ptOwner,  
   [out] DWORD           *reserved,  
   [out] LPWSTR          wzName,  
   [in]  ULONG           cchName,  
   [out] ULONG           *pchName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `gp`  
 からメタデータを返す対象のジェネリックパラメーターを表すトークン。  
  
 `pulParamSeq`  
 入出力`Type`親コンストラクターまたはメソッド内のパラメーターの序数位置。  
  
 `pdwParamFlags`  
 入出力ジェネリックパラメーターのを記述する[Corgenericparamattr](corgenericparamattr-enumeration.md)列挙体の値 `Type` 。  
  
 `ptOwner`  
 入出力パラメーターの所有者を表す TypeDef または MethodDef トークン。  
  
 `reserved`  
 入出力将来の拡張のために予約されています。  
  
 `wzName`  
 入出力ジェネリックパラメーターの名前。  
  
 `cchName`  
 からバッファーのサイズ `wzName` 。  
  
 `pchName`  
 入出力名前の返されたサイズ (ワイド文字単位)。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
