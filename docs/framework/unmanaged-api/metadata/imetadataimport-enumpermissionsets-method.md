---
title: IMetaDataImport::EnumPermissionSets メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.EnumPermissionSets
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::EnumPermissionSets
helpviewer_keywords:
- EnumPermissionSets method [.NET Framework metadata]
- IMetaDataImport::EnumPermissionSets method [.NET Framework metadata]
ms.assetid: 347d7e5c-c90f-45ad-bd1e-2c7912b0b19c
topic_type:
- apiref
ms.openlocfilehash: 79b1493d262288c1d85a56538810e35a73441595
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84491764"
---
# <a name="imetadataimportenumpermissionsets-method"></a>IMetaDataImport::EnumPermissionSets メソッド
指定したメタデータ スコープ内のオブジェクトのアクセス許可を列挙します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumPermissionSets  
   [in, out] HCORENUM      *phEnum,
   [in]      mdToken       tk,
   [in]      DWORD         dwActions,  
   [out]     mdPermission  rPermission[],  
   [in]      ULONG         cMax,  
   [out]     ULONG         *pcTokens  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `phEnum`  
 [入力、出力]列挙子へのポインター。 このメソッドの最初の呼び出しでは、この値は NULL である必要があります。  
  
 `tk`  
 から検索範囲を制限するメタデータトークン。または、可能な限り広い範囲を検索する場合は NULL。  
  
 `dwActions`  
 から<xref:System.Security.Permissions.SecurityAction>に含める値を表すフラグ `rPermission` 。すべてのアクションを返す場合は0。  
  
 `rPermission`  
 入出力アクセス許可トークンを格納するために使用される配列。  
  
 `cMax`  
 [in] `rPermission` 配列の最大サイズ。  
  
 `pcTokens`  
 入出力で返されたアクセス許可トークンの数 `rPermission` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|`S_OK`|`EnumPermissionSets`正常に返されました。|  
|`S_FALSE`|列挙するトークンがありません。 この場合、 `pcTokens` は0になります。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
