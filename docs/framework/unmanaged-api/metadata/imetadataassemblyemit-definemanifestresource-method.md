---
title: IMetaDataAssemblyEmit::DefineManifestResource メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.DefineManifestResource
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::DefineManifestResource
helpviewer_keywords:
- DefineManifestResource method [.NET Framework metadata]
- IMetaDataAssemblyEmit::DefineManifestResource method [.NET Framework metadata]
ms.assetid: 27f6d295-0fe9-4cda-b77e-6e7d5c53df09
topic_type:
- apiref
ms.openlocfilehash: 026f5efe195cdb34999b65c5f47de6f68d30e11a
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008132"
---
# <a name="imetadataassemblyemitdefinemanifestresource-method"></a>IMetaDataAssemblyEmit::DefineManifestResource メソッド
指定したマニフェスト リソースのメタデータを含む `ManifestResource` 構造体を作成し、関連付けられたメタデータ トークンを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineManifestResource (  
    [in] LPCWSTR                szName,
    [in] mdToken                tkImplementation,
    [in] DWORD                  dwOffset,
    [in] DWORD                  dwResourceFlags,  
    [out] mdManifestResource    *pmdmr  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szName`  
 からリソースの名前。  
  
 `tkImplementation`  
 から`mdtFile`リソースプロバイダーにマップされる型またはのメタデータトークン `mdtAssemblyRef` 。 NULL 値は、メタデータが埋め込まれているファイルがリソースプロバイダーであることを示します。  
  
 `dwOffset`  
 からファイル内のリソースの先頭へのオフセット。 スタンドアロンファイルのリソースの場合、この値は常に0になります。 リソースが PE (ポータブル実行可能ファイル) ファイルに埋め込まれている場合、これはリソース BLOB のオフセットになります。これは、cor ヘッダーファイルで指定された場所から開始されます。  
  
 `dwResourceFlags`  
 からリソース定義のプロパティ設定を指定するフラグ値のビットごとの組み合わせ。  
  
 `pmdmr`  
 入出力返されたメタデータトークンへのポインター。  
  
## <a name="remarks"></a>コメント  
 `ManifestResource`各アセンブリのファイルに実装されている各リソースに対して、1つのメタデータ構造を定義する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataAssemblyEmit インターフェイス](imetadataassemblyemit-interface.md)
