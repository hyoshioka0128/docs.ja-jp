---
title: IMetaDataDispenserEx::FindAssemblyModule メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.FindAssemblyModule
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::FindAssemblyModule
helpviewer_keywords:
- FindAssemblyModule method [.NET Framework metadata]
- IMetaDataDispenserEx::FindAssemblyModule method [.NET Framework metadata]
ms.assetid: d1fb65e1-7e19-4513-85b1-44f87c294d3e
topic_type:
- apiref
ms.openlocfilehash: 64f1e2a8f05616c7ca84bc130428629b1176e985
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84006182"
---
# <a name="imetadatadispenserexfindassemblymodule-method"></a>IMetaDataDispenserEx::FindAssemblyModule メソッド
このメソッドは実装されていません。 呼び出された場合は E_NOTIMPL を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT FindAssemblyModule(  
    [in]  LPCWSTR  szAppBase,  
    [in]  LPCWSTR  szPrivateBin,  
    [in]  LPCWSTR  szGlobalBin,  
    [in]  LPCWSTR  szAssemblyName,  
    [in]  LPCWSTR  szModuleName,  
    [out] LPCWSTR  szName,  
    [in]  ULONG    cchName,  
    [out] ULONG    *pcName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `szAppBase`  
 から使用しません。  
  
 `szPrivateBin`  
 から使用しません。  
  
 `szGlobalBin`  
 から使用しません。  
  
 `szAssemblyName`  
 からモジュールの名前。  
  
 `szModuleName`  
 から検索するアセンブリ。  
  
 `szName`  
 入出力アセンブリの簡易名。  
  
 `cchName`  
 からのサイズ (バイト単位) `szName` 。  
  
 `pcName`  
 入出力で実際に返された文字数 `szName` 。  
  
## <a name="requirements"></a>必要条件  
 **プラットフォーム:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataDispenserEx インターフェイス](imetadatadispenserex-interface.md)
- [IMetaDataDispenser インターフェイス](imetadatadispenser-interface.md)
