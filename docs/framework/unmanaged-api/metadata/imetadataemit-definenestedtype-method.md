---
title: IMetaDataEmit::DefineNestedType メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineNestedType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineNestedType
helpviewer_keywords:
- IMetaDataEmit::DefineNestedType method [.NET Framework metadata]
- DefineNestedType method [.NET Framework metadata]
ms.assetid: 1e994de6-4628-459c-b967-b34be1e9fe4f
topic_type:
- apiref
ms.openlocfilehash: 2b24c2ca6907dfdb63ad934ec30557c246db174c
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84004356"
---
# <a name="imetadataemitdefinenestedtype-method"></a>IMetaDataEmit::DefineNestedType メソッド
型定義のメタデータシグネチャを作成し、 `mdTypeDef` その型のトークンを返します。また、定義された型がパラメーターによって参照される型のメンバーであることを指定し `tdEncloser` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineNestedType (
    [in]  LPCWSTR     szTypeDef,  
    [in]  DWORD       dwTypeDefFlags,
    [in]  mdToken     tkExtends,
    [in]  mdToken     rtkImplements[],
    [in]  mdTypeDef   tdEncloser,
    [out] mdTypeDef   *ptd  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szTypeDef`  
 からUnicode での型の名前。  
  
 `dwTypeDefFlags`  
 [入力] `TypeDef`アトリビュート. これは、値のビットマスクです `CorTypeAttr` 。  
  
 `tkExtends`  
 から基本クラスのトークン。 これは、 `mdTypeDef` またはトークンのいずれか `mdTypeRef` です。  
  
 `rtkImplements`[]  
 からこのクラスまたはインターフェイスが実装するインターフェイスを指定するトークンの配列。  
  
 `tdEncloser`  
 から外側の型のトークン。 配列の最後の要素は、である必要があり `mdTokenNil` ます。  
  
 `ptd`  
 入出力`mdTypeDef`割り当てられたトークン。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
