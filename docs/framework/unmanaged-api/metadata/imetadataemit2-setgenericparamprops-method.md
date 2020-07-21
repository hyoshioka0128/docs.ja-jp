---
title: IMetaDataEmit2::SetGenericParamProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit2.SetGenericParamProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit2::SetGenericParamProps
helpviewer_keywords:
- IMetaDataEmit2::SetGenericParamProps method [.NET Framework metadata]
- SetGenericParamProps method [.NET Framework metadata]
ms.assetid: cd93a48d-1fed-4706-bec6-a05dc3b64fbd
topic_type:
- apiref
ms.openlocfilehash: 8feba8e67f3a90dd48fd957065a9c166c204b87c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84492735"
---
# <a name="imetadataemit2setgenericparamprops-method"></a>IMetaDataEmit2::SetGenericParamProps メソッド
指定したトークンによって参照されるジェネリックパラメーター定義のプロパティ値を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetGenericParamProps (  
    [in] mdGenericParam   gp,
    [in] DWORD            dwParamFlags,
    [in] LPCWSTR          szName,
    [in] DWORD            reserved,
    [in] mdToken          rtkConstraints[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `gp`  
 から値を設定するジェネリックパラメーター定義のトークン。  
  
 `dwParamFlags`  
 からジェネリックパラメーターの型を記述する[Corgenericparamattr](corgenericparamattr-enumeration.md)列挙体の値。  
  
 `szName`  
 [in] オプション。 値を設定するパラメーターの名前。  
  
 `reserved`  
 [入力] 将来の機能拡張に備えて予約されています。  
  
 `rtkConstraints`  
 [in] オプション。 型制約の0から終わる配列。 配列メンバーは `mdTypeDef` 、、 `mdTypeRef` 、またはメタデータトークンである必要があり `mdTypeSpec` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
