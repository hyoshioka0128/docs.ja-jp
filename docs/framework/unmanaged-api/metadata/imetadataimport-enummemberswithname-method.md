---
title: IMetaDataImport::EnumMembersWithName メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMembersWithName
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMembersWithName
helpviewer_keywords:
- IMetaDataImport::EnumMembersWithName method [.NET Framework metadata]
- EnumMembersWithName method [.NET Framework metadata]
ms.assetid: 7c9e9120-3104-42f0-86ce-19a025f20dcc
topic_type:
- apiref
ms.openlocfilehash: ea451bdd645d2d4dea4c5dd00408e0bc51804803
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84492071"
---
# <a name="imetadataimportenummemberswithname-method"></a>IMetaDataImport::EnumMembersWithName メソッド
指定した名前を持つ指定した型のメンバーを表す MemberDef トークンを列挙します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumMembersWithName (  
   [in, out] HCORENUM    *phEnum,
   [in]      mdTypeDef   cl,
   [in]      LPCWSTR     szName,
   [out]     mdToken     rMembers[],
   [in]      ULONG       cMax,
   [out]     ULONG       *pcTokens  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `phEnum`  
 [入力、出力]列挙子へのポインター。  
  
 `cl`  
 から列挙するメンバーを持つ型を表す TypeDef トークン。  
  
 `szName`  
 から列挙子のスコープを制限するメンバー名。  
  
 `rMembers`  
 入出力MemberDef トークンを格納するために使用される配列。  
  
 `cMax`  
 [in] `rMembers` 配列の最大サイズ。  
  
 `pcTokens`  
 入出力で返された MemberDef トークンの実際の数 `rMembers` 。  
  
## <a name="remarks"></a>解説  
 このメソッドは、フィールドとメソッドを列挙しますが、プロパティやイベントは列挙しません。 [IMetaDataImport:: EnumMembers](imetadataimport-enummembers-method.md)とは異なり、では、 `EnumMembersWithName` 指定された名前のないすべてのフィールドとメンバートークンが破棄されます。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|`S_OK`|`EnumTypeDefs`正常に返されました。|  
|`S_FALSE`|列挙する MemberDef トークンがありません。 この場合、 `pcTokens` は0になります。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
