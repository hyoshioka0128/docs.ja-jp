---
title: IMetaDataEmit::SetPinvokeMap メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetPinvokeMap
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetPinvokeMap
helpviewer_keywords:
- IMetaDataEmit::SetPinvokeMap method [.NET Framework metadata]
- SetPinvokeMap method [.NET Framework metadata]
ms.assetid: c6bfd574-1da3-4ba7-82f2-46ca5efcbaba
topic_type:
- apiref
ms.openlocfilehash: 0d34c7a2992a2779b96ec87f1a0175d8fcbce34a
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007794"
---
# <a name="imetadataemitsetpinvokemap-method"></a>IMetaDataEmit::SetPinvokeMap メソッド
[IMetaDataEmit::D efinepinvokemap](imetadataemit-definepinvokemap-method.md)の前の呼び出しで定義されているように、メソッドの PInvoke 署名の機能を設定または変更します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetPinvokeMap (
    [in]  mdToken      tk,
    [in]  DWORD        dwMappingFlags,  
    [in]  LPCWSTR      szImportName,
    [in]  mdModuleRef  mrImportDLL
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tk`  
 から`mdToken`マッピング情報が適用される。  
  
 `dwMappingFlags`  
 からマッピングを行うために PInvoke によって使用されるフラグ。 これは、値のビットマスクです `CorPinvokeMap` 。  
  
 `szImportName`  
 からネイティブ DLL 内のターゲットエクスポートの名前。  
  
 `mrImportDLL`  
 から`mdModuleRef`ターゲットのアンマネージ DLL のトークン。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
