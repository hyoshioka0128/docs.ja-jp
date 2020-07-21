---
title: IMetaDataEmit::Merge メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.Merge
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::Merge
helpviewer_keywords:
- IMetaDataEmit::Merge method [.NET Framework metadata]
- Merge method [.NET Framework metadata]
ms.assetid: 7596220c-f699-4b6c-8ae7-c83220610650
topic_type:
- apiref
ms.openlocfilehash: e7fe5cbe27c0771a71e4c03d14ab68ada7d0741a
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84004193"
---
# <a name="imetadataemitmerge-method"></a>IMetaDataEmit::Merge メソッド
マージするスコープの一覧に、指定したインポートされたスコープを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Merge (
    [in]  IMetaDataImport  *pImport,
    [in]  IMapToken        *pHostMapToken,
    [in]  IUnknown         *pHandler
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pImport`  
 からマージするインポートされたスコープを識別する[IMetaDataImport](imetadataimport-interface.md)オブジェクトへのポインター。  
  
 `pIMap`  
 からトークンの再マップを指定する[IMapToken](imaptoken-interface.md)オブジェクトへのポインター。  
  
 `pHandler`  
 からエラーを指定する[IUnknown](/cpp/atl/iunknown)オブジェクトへのポインター。  
  
## <a name="remarks"></a>コメント  
 [IMetaDataEmit:: MergeEnd](imetadataemit-mergeend-method.md)を呼び出して、メタデータの1つのスコープへのマージをトリガーします。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
