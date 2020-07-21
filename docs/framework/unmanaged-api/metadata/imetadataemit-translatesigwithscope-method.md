---
title: IMetaDataEmit::TranslateSigWithScope メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.TranslateSigWithScope
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::TranslateSigWithScope
helpviewer_keywords:
- TranslateSigWithScope method [.NET Framework metadata]
- IMetaDataEmit::TranslateSigWithScope method [.NET Framework metadata]
ms.assetid: 47915d33-b7bf-409e-b484-4ee1df15de22
topic_type:
- apiref
ms.openlocfilehash: 7ef6dbc46806febc6fba89b39a8b894377225c23
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84003970"
---
# <a name="imetadataemittranslatesigwithscope-method"></a>IMetaDataEmit::TranslateSigWithScope メソッド
現在のスコープにアセンブリをインポートし、マージされたスコープの新しいメタデータシグネチャを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT TranslateSigWithScope (
    [in]  IMetaDataAssemblyImport   *pAssemImport,
    [in]  const void                *pbHashValue,
    [in]  ULONG                     cbHashValue,
    [in]  IMetaDataImport           *import,
    [in]  PCCOR_SIGNATURE           pbSigBlob,
    [in]  ULONG                     cbSigBlob,  
    [in]  IMetaDataAssemblyEmit     *pAssemEmit,
    [in]  IMetaDataEmit             *emit,
    [out] PCOR_SIGNATURE            pvTranslatedSig,
    [in]  ULONG                     cbTranslatedSigMax,
    [out] ULONG                     *pcbTranslatedSig
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAssemImport`  
 からインポートアセンブリのインターフェイス (シグネチャが定義されている場合)。  
  
 `pbHashValue`  
 からアセンブリのハッシュ blob。  
  
 `cbHashValue`  
 からのバイト数 `pbHashValue` 。  
  
 `import`  
 からインポートメタデータスコープのインターフェイス。  
  
 `pbSigBlob`  
 からインポートされる署名。  
  
 `cbSigBlob`  
 からのサイズ (バイト単位) `pbSigBlob` 。  
  
 `pAssemEmit`  
 からエクスポートアセンブリのインターフェイス。  
  
 `emit`  
 からエクスポートメタデータスコープのインターフェイス。  
  
 `pvTranslatedSig`  
 入出力変換された署名 blob を保持するバッファー。  
  
 `cbTranslatedSigMax`  
 からの容量 (バイト単位) `pvTranslatedSig` 。  
  
 `pcbTranslatedSig`  
 入出力変換されたシグネチャの実際のバイト数。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataAssemblyEmit インターフェイス](imetadataassemblyemit-interface.md)
- [IMetaDataAssemblyImport インターフェイス](imetadataassemblyimport-interface.md)
- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
