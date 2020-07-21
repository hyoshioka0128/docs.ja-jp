---
title: IMetaDataImport::FindMemberRef メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMemberRef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMemberRef
helpviewer_keywords:
- IMetaDataImport::FindMemberRef method [.NET Framework metadata]
- FindMemberRef method [.NET Framework metadata]
ms.assetid: 1ccda329-d752-4d89-abe8-511af3c3f4c9
topic_type:
- apiref
ms.openlocfilehash: 068014732cee91147edaec29fa0f954a741d8b5c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491655"
---
# <a name="imetadataimportfindmemberref-method"></a>IMetaDataImport::FindMemberRef メソッド
指定した <xref:System.Type> と指定した名前とメタデータシグネチャを持つメンバー参照の MemberRef トークンへのポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT FindMemberRef (  
   [in]  mdTypeRef          td,  
   [in]  LPCWSTR            szName,
   [in]  PCCOR_SIGNATURE    pvSigBlob,
   [in]  ULONG              cbSigBlob,
   [out] mdMemberRef        *pmr  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `td`  
 から検索対象のメンバー参照を囲むクラスまたはインターフェイスの TypeRef トークン。 この値がの場合 `mdTokenNil` 、グローバル変数またはグローバル関数参照に対して参照が行われます。  
  
 `szName`  
 から検索対象のメンバー参照の名前。  
  
 `pvSigBlob`  
 からメンバー参照のバイナリメタデータシグネチャへのポインター。  
  
 `cbSigBlob`  
 からのサイズ (バイト単位) `pvSigBlob` 。  
  
 `pmr`  
 入出力一致する MemberRef トークンへのポインター。  
  
## <a name="remarks"></a>解説  
 メンバーは、外側のクラスまたはインターフェイス ( `td` )、その名前 ( `szName` )、および必要に応じてシグネチャ () を使用して指定し `pvSigBlob` ます。  
  
 署名は特定のスコープにバインドされるため、に渡されるシグネチャは、 `FindMemberRef` 現在のスコープで生成される必要があります。 署名には、外側のクラスまたは値の型を識別するトークンを埋め込むことができます。 トークンは、ローカルの TypeDef テーブルのインデックスです。 現在のスコープのコンテキスト外でランタイムシグネチャを作成し、その署名をへの入力として使用することはできません `FindMemberRef` 。  
  
 `FindMemberRef`クラスまたはインターフェイスで直接定義されたメンバー参照だけを検索します。継承されたメンバー参照は見つかりません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
