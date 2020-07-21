---
title: IMetaDataImport::GetTypeSpecFromToken メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetTypeSpecFromToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetTypeSpecFromToken
helpviewer_keywords:
- GetTypeSpecFromToken method [.NET Framework metadata]
- IMetaDataImport::GetTypeSpecFromToken method [.NET Framework metadata]
ms.assetid: ee518bda-3296-482e-a7b7-e9d51dd1a181
topic_type:
- apiref
ms.openlocfilehash: 43e9671afa92d36966e51bbdc630db4a9d9083b7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503505"
---
# <a name="imetadataimportgettypespecfromtoken-method"></a>IMetaDataImport::GetTypeSpecFromToken メソッド
指定したトークンが表すタイプ仕様のバイナリ メタデータ シグネチャを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTypeSpecFromToken (
   [in]  mdTypeSpec            typespec,
   [out] PCCOR_SIGNATURE       *ppvSig,
   [out] ULONG                 *pcbSig  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `typespec`  
 から要求されたメタデータ署名に関連付けられている TypeSpec トークン。  
  
 `ppvSig`  
 入出力バイナリメタデータシグネチャへのポインター。  
  
 `pcbSig`  
 入出力メタデータシグネチャのサイズ (バイト単位)。  
  
## <a name="return-value"></a>戻り値  
 成功または失敗を示す HRESULT。 失敗したマクロを使用してエラーをテストできます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
