---
title: IMetaDataEmit::DefinePinvokeMap メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefinePinvokeMap
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefinePinvokeMap
helpviewer_keywords:
- DefinePinvokeMap method [.NET Framework metadata]
- IMetaDataEmit::DefinePinvokeMap method [.NET Framework metadata]
ms.assetid: 03abf921-5154-4070-88fa-10b7092901fb
topic_type:
- apiref
ms.openlocfilehash: 447ec44ed3efc4eec84d1e4acd6f2ec1a730bf74
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008028"
---
# <a name="imetadataemitdefinepinvokemap-method"></a>IMetaDataEmit::DefinePinvokeMap メソッド
指定したトークンによって参照されるメソッドの PInvoke 署名の特徴を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefinePinvokeMap (
    [in]  mdToken            tk,
    [in]  DWORD              dwMappingFlags,
    [in]  LPCWSTR            szImportName,
    [in]  mdModuleRef        mrImportDLL
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tk`  
 からターゲットメソッドのトークン。  
  
 `dwMappingFlags`  
 からマッピングを行うために PInvoke によって使用されるフラグ。  
  
 `szImportName`  
 からアンマネージ DLL 内の対象のエクスポートメソッドの名前。  
  
 `mrImportDLL`  
 からターゲットのネイティブ DLL のトークン。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
