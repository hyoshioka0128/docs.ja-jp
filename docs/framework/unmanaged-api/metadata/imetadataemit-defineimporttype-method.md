---
title: IMetaDataEmit::DefineImportType メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineImportType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineImportType
helpviewer_keywords:
- DefineImportType method [.NET Framework metadata]
- IMetaDataEmit::DefineImportType method [.NET Framework metadata]
ms.assetid: 37fd27af-8062-4904-ace4-51bb78ec600a
topic_type:
- apiref
ms.openlocfilehash: edce5cb93b770fb5730e5a06633ffffacf332f7a
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84004694"
---
# <a name="imetadataemitdefineimporttype-method"></a>IMetaDataEmit::DefineImportType メソッド
現在のスコープの外部で定義されている指定した型への参照を作成し、その参照のトークンを定義します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineImportType (
    [in]  IMetaDataAssemblyImport  *pAssemImport,
    [in]  const void               *pbHashValue,
    [in]  ULONG                    cbHashValue,
    [in]  IMetaDataImport          *pImport,
    [in]  mdTypeDef                tdImport,
    [in]  IMetaDataAssemblyEmit    *pAssemEmit,
    [out] mdTypeRef                *ptr  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAssemImport`  
 から対象の型のインポート元のアセンブリを表す[IMetaDataAssemblyImport](imetadataassemblyimport-interface.md)インターフェイス。  
  
 `pbHashValue`  
 からによって指定されたアセンブリのハッシュを格納している配列 `pAssemImport` 。  
  
 `cbHashValue`  
 [in] `pbHashValue` 配列のバイト数。  
  
 `pImport`  
 から対象の型のインポート元のメタデータスコープを表す[IMetaDataImport](imetadataimport-interface.md)インターフェイス。  
  
 `tdImport`  
 から`mdTypeDef`対象の型を指定するトークンです。  
  
 `pAssemEmit`  
 からターゲット型がインポートされるアセンブリを表す[IMetaDataAssemblyEmit](imetadataassemblyemit-interface.md)インターフェイス。  
  
 `ptr`  
 入出力`mdTypeRef`型参照の現在のスコープで定義されているトークン。  
  
## <a name="remarks"></a>コメント  
 [IMetaDataEmit::D efineImportMember](imetadataemit-defineimportmember-method.md)メソッドを呼び出す前に、メソッドを使用して、 `DefineImportType` メンバーの親クラスまたは親インターフェイスの型参照を現在のスコープ内に作成できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
