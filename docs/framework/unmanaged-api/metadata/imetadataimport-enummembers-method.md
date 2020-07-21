---
title: IMetaDataImport::EnumMembers メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumMembers
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumMembers
helpviewer_keywords:
- IMetaDataImport::EnumMembers method [.NET Framework metadata]
- EnumMembers method [.NET Framework metadata]
ms.assetid: 3fb8e178-342b-4c89-9bcf-f7f834e6cb77
topic_type:
- apiref
ms.openlocfilehash: cc3bc5140da0634b5172f6253de3de37bff487f1
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84492036"
---
# <a name="imetadataimportenummembers-method"></a>IMetaDataImport::EnumMembers メソッド
指定した型のメンバーを表す MemberDef トークンを列挙します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumMembers (
   [in, out]  HCORENUM    *phEnum,
   [in]  mdTypeDef   cl,
   [out] mdToken     rMembers[],
   [in]  ULONG       cMax,
   [out] ULONG       *pcTokens  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `phEnum`  
 [入力、出力]列挙子へのポインター。  
  
 `cl`  
 からメンバーを列挙する型を表す TypeDef トークン。  
  
 `rMembers`  
 入出力MemberDef トークンを保持するために使用される配列。  
  
 `cMax`  
 [in] `rMembers` 配列の最大サイズ。  
  
 `pcTokens`  
 入出力で返された MemberDef トークンの実際の数 `rMembers` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|`S_OK`|`EnumMembers`正常に返されました。|  
|`S_FALSE`|列挙する MemberDef トークンがありません。 この場合、 `pcTokens` は0になります。|  
  
## <a name="remarks"></a>解説  
 クラスのメンバーのコレクションを列挙するときに、 `EnumMembers` クラスで直接定義されたメンバー (プロパティまたはイベントでは**ない**) のみを返します。 クラスが継承されたメンバーの実装を提供している場合でも、クラスが継承するメンバーは返しません。 継承されたメンバーを列挙するには、呼び出し元が継承チェーンを明示的にウォークする必要があります。 継承チェーンの規則は、元のメタデータを出力した言語またはコンパイラによって異なる場合があることに注意してください。

 プロパティとイベントは、によって列挙されません `EnumMembers` 。 これらを列挙するには、 [Enumproperties](imetadataimport-enumproperties-method.md)または[enumproperties](imetadataimport-enumevents-method.md)を使用します。
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
