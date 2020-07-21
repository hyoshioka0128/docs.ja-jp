---
title: IMetaDataImport2::GetMethodSpecProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport2.GetMethodSpecProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport2::GetMethodSpecProps
helpviewer_keywords:
- GetMethodSpecProps method [.NET Framework metadata]
- IMetaDataImport2::GetMethodSpecProps method [.NET Framework metadata]
ms.assetid: 9544b711-e669-4eaf-8630-ee862e5e4489
topic_type:
- apiref
ms.openlocfilehash: 079d9245526ff7914d1cbd6a91f0f2d96a690af5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490446"
---
# <a name="imetadataimport2getmethodspecprops-method"></a>IMetaDataImport2::GetMethodSpecProps メソッド
指定した MethodSpec トークンによって参照されるメソッドのメタデータシグネチャを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMethodSpecProps (  
   [in]  mdMethodSpec     mi,  
   [out] mdToken          *tkParent,  
   [out] PCCOR_SIGNATURE  *ppvSigBlob,
   [out] ULONG            *pcbSigBlob  
);
```  
  
## <a name="parameters"></a>パラメーター  
 `mi`  
 からメソッドのインスタンス化を表す MethodSpec トークン。  
  
 `tkParent`  
 入出力メソッド定義を表す MethodDef または MethodRef トークンへのポインター。  
  
 `ppvSigBlob`  
 入出力メソッドのバイナリメタデータシグネチャへのポインター。  
  
 `pcbSigBlob`  
 入出力のサイズ (バイト単位) `ppvSigBlob` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
