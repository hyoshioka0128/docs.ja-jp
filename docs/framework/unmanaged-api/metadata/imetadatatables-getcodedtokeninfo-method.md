---
title: IMetaDataTables::GetCodedTokenInfo メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataTables.GetCodedTokenInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetCodedTokenInfo
helpviewer_keywords:
- GetCodedTokenInfo method [.NET Framework metadata]
- IMetaDataTables::GetCodedTokenInfo method [.NET Framework metadata]
ms.assetid: 31214d3a-715e-49af-92b3-0fd11e4f218a
topic_type:
- apiref
ms.openlocfilehash: 8ab16ad5b2b2838125e07511ef47be737f40671c
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501210"
---
# <a name="imetadatatablesgetcodedtokeninfo-method"></a>IMetaDataTables::GetCodedTokenInfo メソッド
指定した行インデックスに関連付けられているトークンの配列へのポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCodedTokenInfo (
    [in]  ULONG       ixCdTkn,  
    [out] ULONG       *pcTokens,  
    [out] ULONG       **ppTokens,  
    [out] const char  **ppName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ixCdTkn`  
 から返されるコード化されたトークンの種類。  
  
 `pcTokens`  
 入出力の長さへのポインター `ppTokens` 。  
  
 `ppTokens`  
 入出力返されたトークンのリストを格納する配列へのポインターへのポインター。  
  
 `ppName`  
 入出力にあるトークンの名前へのポインターへのポインター `ixCdTkn` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataTables インターフェイス](imetadatatables-interface.md)
- [IMetaDataTables2 インターフェイス](imetadatatables2-interface.md)
