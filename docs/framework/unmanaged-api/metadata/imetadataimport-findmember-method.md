---
title: IMetaDataImport::FindMember メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMember
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMember
helpviewer_keywords:
- IMetaDataImport::FindMember method [.NET Framework metadata]
- FindMember method [.NET Framework metadata]
ms.assetid: ad32fb84-c2b6-41cd-888d-787ff3a90449
topic_type:
- apiref
ms.openlocfilehash: fce4f3875fbdb110134d6b7f684eff40821f6bdd
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503680"
---
# <a name="imetadataimportfindmember-method"></a>IMetaDataImport::FindMember メソッド
指定した <xref:System.Type> と指定した名前とメタデータシグネチャを持つフィールドまたはメソッドの MemberDef トークンへのポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT FindMember (  
   [in]  mdTypeDef         td,  
   [in]  LPCWSTR           szName,
   [in]  PCCOR_SIGNATURE   pvSigBlob,
   [in]  ULONG             cbSigBlob,
   [out] mdToken           *pmb  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `td`  
 から検索対象のメンバーを囲むクラスまたはインターフェイスの TypeDef トークン。 この値がの場合 `mdTokenNil` 、グローバル変数またはグローバル関数の参照が行われます。  
  
 `szName`  
 から検索対象のメンバーの名前。  
  
 `pvSigBlob`  
 からメンバーのバイナリメタデータシグネチャへのポインター。  
  
 `cbSigBlob`  
 からのサイズ (バイト単位) `pvSigBlob` 。  
  
 `pmb`  
 入出力一致する MemberDef トークンへのポインター。  
  
## <a name="remarks"></a>解説  
 メンバーは、外側のクラスまたはインターフェイス ( `td` )、その名前 ( `szName` )、および必要に応じてシグネチャ () を使用して指定し `pvSigBlob` ます。 クラスまたはインターフェイスに同じ名前のメンバーが複数存在する可能性があります。 その場合は、メンバーのシグネチャを渡して、一意の一致を検索します。  
  
 署名は特定のスコープにバインドされるため、に渡されるシグネチャは、 `FindMember` 現在のスコープで生成される必要があります。 署名には、外側のクラスまたは値の型を識別するトークンを埋め込むことができます。 トークンは、ローカルの TypeDef テーブルのインデックスです。 現在のスコープのコンテキスト外でランタイムシグネチャを作成し、その署名を入力として使用してへの入力として使用することはできません `FindMember` 。  
  
 `FindMember`クラスまたはインターフェイスで直接定義されたメンバーのみを検索します。継承されたメンバーは見つかりません。  
  
> [!NOTE]
> `FindMember`は、ヘルパーメソッドです。 [IMetaDataImport:: FindMethod](imetadataimport-findmethod-method.md); を呼び出します。この呼び出しで一致するものが見つからない場合は、 `FindMember` [IMetaDataImport:: findfield](imetadataimport-findfield-method.md)を呼び出します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
