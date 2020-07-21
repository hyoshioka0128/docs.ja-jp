---
title: IMetaDataEmit::DefineTypeRefByName メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineTypeRefByName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineTypeRefByName
helpviewer_keywords:
- DefineTypeRefByName method [.NET Framework metadata]
- IMetaDataEmit::DefineTypeRefByName method [.NET Framework metadata]
ms.assetid: c30a4ce3-2d3e-411a-98df-e62ac4a5dd50
topic_type:
- apiref
ms.openlocfilehash: ae30140e69926be32570960a32524a74b850bda4
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009354"
---
# <a name="imetadataemitdefinetyperefbyname-method"></a>IMetaDataEmit::DefineTypeRefByName メソッド
現在のスコープ外にある、指定されたスコープで定義されている型のメタデータトークンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineTypeRefByName (
    [in]  mdToken     tkResolutionScope,
    [in]  LPCWSTR     szName,
    [out] mdTypeRef   *ptr
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tkResolutionScope`  
 から解決スコープを指定するトークン。 有効なトークンの種類は次のとおりです。  
  
- `mdModuleRef`型が、呼び出し元が定義されている同じアセンブリ内で定義されている場合は。  
  
- `mdAssemblyRef`型が、呼び出し元が定義されているアセンブリ以外のアセンブリで定義されている場合は。  
  
- `mdTypeRef`型が入れ子にされた型の場合は。  
  
- `mdModule`型が、呼び出し元が定義されている同じモジュールで定義されている場合は。  
  
- 型がグローバルに定義されている場合は Null。  
  
 `szName`  
 からUnicode での対象の型の名前。  
  
 `ptr`  
 入出力`mdTypeRef`型に割り当てられているトークンへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
