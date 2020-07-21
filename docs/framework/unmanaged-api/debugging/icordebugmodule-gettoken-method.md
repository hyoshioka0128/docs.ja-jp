---
title: ICorDebugModule::GetToken メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugModule.GetToken
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::GetToken
helpviewer_keywords:
- ICorDebugModule::GetToken method [.NET Framework debugging]
- GetToken method, ICorDebugModule interface [.NET Framework debugging]
ms.assetid: f759f87a-18ae-4c1a-8300-29b803432d0a
topic_type:
- apiref
ms.openlocfilehash: 1cf4d82200709971201da60d06d0cb929641a104
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501886"
---
# <a name="icordebugmodulegettoken-method"></a>ICorDebugModule::GetToken メソッド
このモジュールのテーブルエントリのトークンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetToken(  
    [out] mdModule *pToken  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pToken`  
 入出力`mdModule`モジュールのメタデータを参照するトークンへのポインター。  
  
## <a name="remarks"></a>解説  
 トークンは、 [IMetaDataImport](../metadata/imetadataimport-interface.md)、 [IMetaDataImport2](../metadata/imetadataimport2-interface.md)、および[IMetaDataAssemblyImport](../metadata/imetadataassemblyimport-interface.md)メタデータインポートインターフェイスに渡すことができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [Metadata](../metadata/index.md)
