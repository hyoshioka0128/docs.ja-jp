---
title: IMetaDataEmit::DefineImportMember メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineImportMember
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineImportMember
helpviewer_keywords:
- DefineImportMember method [.NET Framework metadata]
- IMetaDataEmit::DefineImportMember method [.NET Framework metadata]
ms.assetid: c7dd94c6-335b-46ff-9dfe-505056db5673
topic_type:
- apiref
ms.openlocfilehash: 2facc63023a20dd6aaac64d7d036324c31658bc8
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501314"
---
# <a name="imetadataemitdefineimportmember-method"></a>IMetaDataEmit::DefineImportMember メソッド
現在のスコープの外部で定義されている型またはモジュールの指定したメンバーへの参照を作成し、その参照のトークンを定義します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineImportMember (
    [in]  IMetaDataAssemblyImport  *pAssemImport,
    [in]  const void               *pbHashValue,
    [in]  ULONG                    cbHashValue,  
    [in]  IMetaDataImport          *pImport,
    [in]  mdToken                  mbMember,
    [in]  IMetaDataAssemblyEmit    *pAssemEmit,
    [in]  mdToken                  tkParent,
    [out] mdMemberRef              *pmr
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAssemImport`  
 からターゲットメンバーのインポート元のアセンブリを表す[IMetaDataAssemblyImport](imetadataassemblyimport-interface.md)インターフェイス。  
  
 `pbHashValue`  
 からによって指定されたアセンブリのハッシュを格納している配列 `pAssemImport` 。  
  
 `cbHashValue`  
 [in] `pbHashValue` 配列のバイト数。  
  
 `pImport`  
 からターゲットメンバーのインポート元のメタデータスコープを表す[IMetaDataImport](imetadataimport-interface.md)インターフェイス。  
  
 `mbMember`  
 からターゲットメンバーを指定するメタデータトークン。 トークンには、 `mdMethodDef` (メンバーメソッドの場合)、(メンバープロパティの場合)、 `mdProperty` または `mdFieldDef` (メンバーフィールドの場合) トークンを指定できます。  
  
 `pAssemEmit`  
 からターゲットメンバーがインポートされるアセンブリを表す[IMetaDataAssemblyEmit](imetadataassemblyemit-interface.md)インターフェイス。  
  
 `tkParent`  
 から`mdTypeRef` `mdModuleRef` ターゲットメンバーを所有する型またはモジュールのトークンまたはトークン。  
  
 `pmr`  
 入出力`mdMemberRef`メンバー参照の現在のスコープで定義されているトークン。  
  
## <a name="remarks"></a>解説  
 メソッドは、で指定された `DefineImportMember` メンバーを検索し `mbMember` ます。このメンバーは、で指定した別のスコープで定義され、 `pImport` そのプロパティを取得します。 この情報を使用して、現在のスコープで[IMetaDataEmit::D efinememberref](imetadataemit-definememberref-method.md)メソッドを呼び出し、メンバー参照を作成します。  
  
 一般に、メソッドを使用する前に、 `DefineImportMember` ターゲットメンバーの親クラス、インターフェイス、またはモジュールの型参照またはモジュール参照を、現在のスコープで作成する必要があります。 その後、この参照のメタデータトークンが引数として渡され `tkParent` ます。 後でコンパイラまたはリンカーによって解決される場合は、ターゲットメンバーの親への参照を作成する必要はありません。 まとめ  
  
- ターゲットメンバーがフィールドまたはメソッドの場合は、 [IMetaDataEmit::D efinetyperefbyname](imetadataemit-definetyperefbyname-method.md)または[IMetaDataEmit::D efineImportType](imetadataemit-defineimporttype-method.md)メソッドを使用して、メンバーの親クラスまたは親インターフェイスの型参照を現在のスコープ内に作成します。  
  
- ターゲットメンバーがグローバル変数またはグローバル関数 (つまり、クラスまたはインターフェイスのメンバーではない) である場合は、 [IMetaDataEmit::D efinemoduleref](imetadataemit-definemoduleref-method.md)メソッドを使用して、メンバーの親モジュールに対して、現在のスコープでモジュール参照を作成します。  
  
- ターゲットメンバーの親が、後でコンパイラまたはリンカーによって解決される場合は、を渡し `mdTokenNil` `tkParent` ます。 これが適用される唯一のシナリオは、グローバル関数またはグローバル変数が、最終的に現在のモジュールにリンクされ、メタデータがマージされる .obj ファイルからインポートされる場合です。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
