---
title: IMetaDataConverter::GetMetaDataFromTypeLib メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataConverter.GetMetaDataFromTypeLib
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataConverter::GetMetaDataFromTypeLib
helpviewer_keywords:
- IMetaDataConverter::GetMetaDataFromTypeLib method [.NET Framework metadata]
- GetMetaDataFromTypeLib method [.NET Framework metadata]
ms.assetid: 97dc3a56-adfa-431f-889e-06a35ac84d51
topic_type:
- apiref
ms.openlocfilehash: 8f8c0c2cb8dea8ad2b9c0040654122ef5942aca0
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008392"
---
# <a name="imetadataconvertergetmetadatafromtypelib-method"></a>IMetaDataConverter::GetMetaDataFromTypeLib メソッド
指定したインスタンスによって表されるタイプライブラリのメタデータシグネチャを表す[IMetaDataImport](imetadataimport-interface.md)インスタンスへのインターフェイスポインターを取得し `ITypeLib` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMetaDataFromTypeLib (  
    [in]  ITypeLib        *pITL,
    [out] IMetaDataImport **ppMDI  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pITL`  
 から`ITypeLib`タイプライブラリを表すオブジェクトへのポインター。  
  
 `ppMDI`  
 入出力メタデータシグネチャを表すインスタンスのアドレスを受け取る場所へのポインター `IMetaDataImport` 。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
