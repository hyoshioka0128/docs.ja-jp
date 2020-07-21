---
title: IMetaDataImport::GetModuleRefProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetModuleRefProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetModuleRefProps
helpviewer_keywords:
- GetModuleRefProps method [.NET Framework metadata]
- IMetaDataImport::GetModuleRefProps method [.NET Framework metadata]
ms.assetid: b558e766-4c11-4628-ae47-b4e0a1800168
topic_type:
- apiref
ms.openlocfilehash: f1784c9f3085ce188f9e540887dd02064f8448f3
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503579"
---
# <a name="imetadataimportgetmodulerefprops-method"></a>IMetaDataImport::GetModuleRefProps メソッド
指定したメタデータ トークンによって参照されるモジュールの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetModuleRefProps (  
   [in]  mdModuleRef         mur,  
   [out] LPWSTR              szName,
   [in]  ULONG               cchName,
   [out] ULONG               *pchName
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mur`  
 からメタデータ情報を取得するモジュールを参照する ModuleRef メタデータトークン。  
  
 `szName`  
 入出力モジュール名を保持するバッファー。  
  
 `cchName`  
 から要求されたサイズ ( `szName` ワイド文字単位)。  
  
 `pchName`  
 入出力返されたのサイズを `szName` ワイド文字数で返します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
