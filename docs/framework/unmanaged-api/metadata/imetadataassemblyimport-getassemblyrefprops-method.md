---
title: IMetaDataAssemblyImport::GetAssemblyRefProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyImport.GetAssemblyRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyImport::GetAssemblyRefProps
helpviewer_keywords:
- IMetaDataAssemblyImport::GetAssemblyRefProps method [.NET Framework metadata]
- GetAssemblyRefProps method [.NET Framework metadata]
ms.assetid: 5c6b7fb4-cbca-4479-b650-ab9a99732ea0
topic_type:
- apiref
ms.openlocfilehash: 2858e924ab6effe192955ce53dad9d333d2d244d
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009068"
---
# <a name="imetadataassemblyimportgetassemblyrefprops-method"></a>IMetaDataAssemblyImport::GetAssemblyRefProps メソッド
指定されたメタデータシグネチャを持つアセンブリ参照のプロパティのセットを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAssemblyRefProps (  
    [in]  mdAssemblyRef        mdar,
    [out] const void          **ppbPublicKeyOrToken,
    [out] ULONG                *pcbPublicKeyOrToken,
    [out] LPWSTR               szName,
    [in]  ULONG                cchName,
    [out] ULONG                *pchName,
    [out] ASSEMBLYMETADATA     *pMetaData,
    [out] const void           **ppbHashValue,
    [out] ULONG                *pcbHashValue,
    [out] DWORD                *pdwAssemblyRefFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mdar`  
 から`mdAssemblyRef`プロパティを取得する対象のアセンブリ参照を表すメタデータトークン。  
  
 `ppbPublicKeyOrToken`  
 入出力公開キーまたはメタデータトークンへのポインター。  
  
 `pcbPublicKeyOrToken`  
 入出力返される公開キーまたはトークン内のバイト数。  
  
 `szName`  
 入出力アセンブリの簡易名。  
  
 `cchName`  
 からのサイズ (ワイド文字数) `szName` 。  
  
 `pchName`  
 入出力実際にで返されるワイド文字数へのポインター `szName` 。  
  
 `pMetaData`  
 入出力アセンブリメタデータを格納している ASSEMBLYMETADATA 構造体へのポインター。  
  
 `ppbHashValue`  
 入出力ハッシュ値へのポインター。 これは、参照されるアセンブリのプロパティの SHA-1 アルゴリズムを使用するハッシュです `PublicKey` 。 [Assemblyrefflags](assemblyrefflags-enumeration.md)の列挙の arfFullOriginator フラグが設定されている場合を除きます。  
  
 `pcbHashValue`  
 入出力返されたハッシュ値のワイド文字の数。  
  
 `pdwAssemblyRefFlags`  
 入出力アセンブリに適用されるメタデータを記述するフラグへのポインター。 Flags 値は、1つまたは複数の[Corassemblyflags](corassemblyflags-enumeration.md)値を組み合わせたものです。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、このメソッドは S_OK を返します。それ以外の場合は、Winerror.h ヘッダーファイルで定義されているエラーコードの1つを返します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataAssemblyImport インターフェイス](imetadataassemblyimport-interface.md)
