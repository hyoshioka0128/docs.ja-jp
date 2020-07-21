---
title: IMetaDataImport::GetPinvokeMap メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetPinvokeMap
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetPinvokeMap
helpviewer_keywords:
- IMetaDataImport::GetPinvokeMap method [.NET Framework metadata]
- GetPinvokeMap method [.NET Framework metadata]
ms.assetid: b8685c1e-b80c-4198-8eb3-748d6f48a99e
topic_type:
- apiref
ms.openlocfilehash: 8409e56b5ec4dbe47035a0555b6b7ce175b517ee
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490979"
---
# <a name="imetadataimportgetpinvokemap-method"></a>IMetaDataImport::GetPinvokeMap メソッド
PInvoke 呼び出しの対象アセンブリを表す ModuleRef トークンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetPinvokeMap (  
   [in]  mdToken       tk,  
   [out] DWORD         *pdwMappingFlags,  
   [out] LPWSTR        szImportName,  
   [in]  ULONG         cchImportName,  
   [out] ULONG         *pchImportName,  
   [out] mdModuleRef   *pmrImportDLL  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tk`  
 からPInvoke マッピングメタデータを取得する FieldDef または MethodDef トークン。  
  
 `pdwMappingFlags`  
 入出力マッピングに使用されるフラグへのポインター。 この値は、 [CorPinvokeMap](corpinvokemap-enumeration.md)列挙体のビットマスクです。  
  
 `szImportName`  
 入出力アンマネージターゲット DLL の名前。  
  
 `cchImportName`  
 からのワイド文字のサイズ `szImportName` 。  
  
 `pchImportName`  
 入出力で返されたワイド文字の数 `szImportName` 。  
  
 `pmrImportDLL`  
 入出力アンマネージターゲットオブジェクトライブラリを表す ModuleRef トークンへのポインター。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
