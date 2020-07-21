---
title: IMetaDataAssemblyImport::GetExportedTypeProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetExportedTypeProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetExportedTypeProps
helpviewer_keywords:
- GetExportedTypeProps method [.NET Framework metadata]
- IMetaDataAssemblyImport::GetExportedTypeProps method [.NET Framework metadata]
ms.assetid: 25ca7623-5a55-4f09-b44a-36b03d142278
topic_type:
- apiref
ms.openlocfilehash: 944941c2356cae93ecc85f1714b4b29aefcb50ad
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008405"
---
# <a name="imetadataassemblyimportgetexportedtypeprops-method"></a>IMetaDataAssemblyImport::GetExportedTypeProps メソッド
指定したメタデータシグネチャを持つ、エクスポートされた型のプロパティのセットを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetExportedTypeProps (  
    [in]  mdExportedType    mdct,
    [out] LPWSTR            szName,
    [in]  ULONG             cchName,
    [out] ULONG             *pchName,
    [out] mdToken           *ptkImplementation,
    [out] mdTypeDef         *ptkTypeDef,
    [out] DWORD             *pdwExportedTypeFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mdct`  
 からエクスポートされた `mdExportedType` 型を表すメタデータトークン。  
  
 `szName`  
 入出力エクスポートされた型の名前。  
  
 `cchName`  
 からのサイズ (ワイド文字単位) `szName` 。  
  
 `pchName`  
 入出力実際に返されるワイド文字の数`szName`  
  
 `ptkImplementation`  
 入出力`mdFile` `mdAssemblyRef` エクスポートされた `mdExportedType` 型のプロパティへのアクセスを格納または許可する、、、またはメタデータトークン。  
  
 `ptkTypeDef`  
 入出力`mdTypeDef`ファイル内の型を表すトークンへのポインター。  
  
 `pdwExportedTypeFlags`  
 入出力エクスポートされた型に適用されるメタデータを記述するフラグへのポインター。 Flags 値には、1つまたは複数の[Cortypeattr](cortypeattr-enumeration.md)値を指定できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataAssemblyImport インターフェイス](imetadataassemblyimport-interface.md)
