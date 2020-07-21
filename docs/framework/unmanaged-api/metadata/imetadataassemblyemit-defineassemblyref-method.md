---
title: IMetaDataAssemblyEmit::DefineAssemblyRef メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.DefineAssemblyRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::DefineAssemblyRef
helpviewer_keywords:
- DefineAssemblyRef method [.NET Framework metadata]
- IMetaDataAssemblyEmit::DefineAssemblyRef method [.NET Framework metadata]
ms.assetid: 0b284b18-0084-4b3a-912a-5ebe9f29c88b
topic_type:
- apiref
ms.openlocfilehash: 612463bca18c23fac0b086adde2d208a0fbc5ae5
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008171"
---
# <a name="imetadataassemblyemitdefineassemblyref-method"></a>IMetaDataAssemblyEmit::DefineAssemblyRef メソッド
このアセンブリが参照するアセンブリのメタデータを含む `AssemblyRef` 構造体を作成し、関連付けられたメタデータ トークンを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineAssemblyRef (  
    [in]  void                *pbPublicKeyOrToken,  
    [in]  ULONG               cbPublicKeyOrToken,  
    [in]  LPCWSTR             szName,  
    [in]  ASSEMBLYMETADATA    pMetaData,  
    [in]  void                *pbHashValue,  
    [in]  ULONG               cbHashValue,  
    [in]  DWORD               dwAssemblyRefFlags,  
    [out] mdAssemblyRef       *pmdar  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbPublicKeyOrToken`  
 から参照アセンブリの発行元の公開キー。 ヘルパー関数[StrongNameTokenFromAssembly](../strong-naming/strongnametokenfromassembly-function.md)を使用して、このパラメーターとして渡す公開キーのハッシュを取得できます。  
  
 `cbPublicKeyOrToken`  
 からのサイズ (バイト単位) `pbPublicKeyOrToken` 。  
  
 `szName`  
 からユーザーが判読できる、アセンブリのテキスト名。 この値は、1024文字を超えないようにする必要があります。  
  
 `pMetaData`  
 から参照されたアセンブリのバージョン、プラットフォーム、およびロケール情報を格納している ASSEMBLYMETADATA インスタンス。  
  
 `pbHashValue`  
 から参照アセンブリに関連付けられているハッシュデータ。 省略可能。  
  
 `cbHashValue`  
 からのサイズ (バイト単位) `pbHashValue` 。  
  
 `dwAssemblyRefFlags`  
 から実行エンジンの動作に影響を与える[Corassemblyflags](corassemblyflags-enumeration.md)値のビットごとの組み合わせ。  
  
 `pmdar`  
 入出力返された `AssemblyRef` メタデータトークンへのポインター。  
  
## <a name="remarks"></a>コメント  
 `AssemblyRef`このアセンブリが参照するアセンブリごとに1つのメタデータ構造を定義する必要があります。  
  
 実行時には、参照されたアセンブリの詳細がアセンブリリゾルバーに渡され、"ビルド済み" の情報を表すことが示されます。 次に、アセンブリリゾルバーがポリシーを適用します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataAssemblyEmit インターフェイス](imetadataassemblyemit-interface.md)
