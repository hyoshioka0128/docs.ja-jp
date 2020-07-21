---
title: IMetaDataImport::FindMethod メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.FindMethod
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::FindMethod
helpviewer_keywords:
- FindMethod method [.NET Framework metadata]
- IMetaDataImport::FindMethod method [.NET Framework metadata]
ms.assetid: 0f9bde1d-e306-438d-941b-d0925b322304
topic_type:
- apiref
ms.openlocfilehash: c2ec907759a25048444ebcc81bf5bb0fd23ced58
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503654"
---
# <a name="imetadataimportfindmethod-method"></a>IMetaDataImport::FindMethod メソッド
指定した <xref:System.Type> と指定した名前とメタデータシグネチャを持つメソッドの MethodDef トークンへのポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT FindMethod (  
   [in]  mdTypeDef          td,  
   [in]  LPCWSTR            szName,
   [in]  PCCOR_SIGNATURE    pvSigBlob,
   [in]  ULONG              cbSigBlob,
   [out] mdMethodDef        *pmb  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `td`  
 から検索対象の `mdTypeDef` メンバーを囲む型 (クラスまたはインターフェイス) のトークン。 この値がの場合は `mdTokenNil` 、グローバル関数の参照が行われます。  
  
 `szName`  
 から検索するメソッドの名前。  
  
 `pvSigBlob`  
 からメソッドのバイナリメタデータシグネチャへのポインター。  
  
 `cbSigBlob`  
 からのサイズ (バイト単位) `pvSigBlob` 。  
  
 `pmb`  
 入出力一致する MethodDef トークンへのポインター。  
  
## <a name="remarks"></a>解説  
 メソッドは、外側のクラスまたはインターフェイス ( `td` )、その名前 ( `szName` )、および必要に応じてシグネチャ () を使用して指定し `pvSigBlob` ます。 クラスまたはインターフェイスに同じ名前のメソッドが複数存在する可能性があります。 その場合は、メソッドのシグネチャを渡して、一意の一致を検索します。  
  
 署名は特定のスコープにバインドされるため、に渡されるシグネチャは、 `FindMethod` 現在のスコープで生成される必要があります。 署名には、外側のクラスまたは値の型を識別するトークンを埋め込むことができます。 トークンは、ローカルの TypeDef テーブルのインデックスです。 現在のスコープのコンテキスト外でランタイムシグネチャを作成し、その署名を入力として使用してへの入力として使用することはできません `FindMethod` 。  
  
 `FindMethod`クラスまたはインターフェイスで直接定義されたメソッドのみを検索します。継承されたメソッドは見つかりません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Reflection.MethodInfo>
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
