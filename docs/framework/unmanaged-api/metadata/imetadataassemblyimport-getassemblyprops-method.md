---
title: IMetaDataAssemblyImport::GetAssemblyProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetAssemblyProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetAssemblyProps
helpviewer_keywords:
- GetAssemblyProps method [.NET Framework metadata]
- IMetaDataAssemblyImport::GetAssemblyProps method [.NET Framework metadata]
ms.assetid: 0eaa4aa9-9441-444a-920c-e4b2a2db899e
topic_type:
- apiref
ms.openlocfilehash: a90deaf3e9ddf326c6fca558cbb4681fc40e022d
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009055"
---
# <a name="imetadataassemblyimportgetassemblyprops-method"></a>IMetaDataAssemblyImport::GetAssemblyProps メソッド
指定したメタデータシグネチャを持つアセンブリのプロパティのセットを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAssemblyProps (  
    [in]  mdAssembly          mda,  
    [out] const void          **ppbPublicKey,
    [out] ULONG               *pcbPublicKey,  
    [out] ULONG               *pulHashAlgId,  
    [out] LPWSTR              szName,  
    [in] ULONG                cchName,  
    [out] ULONG               *pchName,  
    [out] ASSEMBLYMETADATA    *pMetaData,  
    [out] DWORD               *pdwAssemblyFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mda`  
 [入力]。 `mdAssembly`プロパティを取得する対象のアセンブリを表すメタデータトークン。  
  
 `ppbPublicKey`  
 入出力公開キーまたはメタデータトークンへのポインター。  
  
 `pcbPublicKey`  
 入出力返される公開キーのバイト数。  
  
 `pulHashAlgId`  
 入出力アセンブリ内のファイルのハッシュに使用されるアルゴリズムへのポインター。  
  
 `szName`  
 入出力アセンブリの簡易名。  
  
 `cchName`  
 からのサイズ (ワイド文字数) `szName` 。  
  
 `pchName`  
 入出力実際にで返されるワイド文字数 `szName` 。  
  
 `pMetaData`  
 入出力アセンブリメタデータを格納している ASSEMBLYMETADATA 構造体へのポインター。  
  
 `pdwAssemblyFlags`  
 入出力アセンブリに適用されるメタデータを記述するフラグ。 この値は、1つまたは複数の[Corassemblyflags](corassemblyflags-enumeration.md)値を組み合わせたものです。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataAssemblyImport インターフェイス](imetadataassemblyimport-interface.md)
