---
title: IMetaDataEmit::SetPermissionSetProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetPermissionSetProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetPermissionSetProps
helpviewer_keywords:
- SetPermissionSetProps method [.NET Framework metadata]
- IMetaDataEmit::SetPermissionSetProps method [.NET Framework metadata]
ms.assetid: 8eaee971-40bf-45e2-a3d8-6e57674213b6
topic_type:
- apiref
ms.openlocfilehash: 1e6ee1f2f497ef30a5390e7afac55c54705248ed
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007807"
---
# <a name="imetadataemitsetpermissionsetprops-method"></a>IMetaDataEmit::SetPermissionSetProps メソッド
[IMetaDataEmit::D efinepermissionset](imetadataemit-definepermissionset-method.md)の前の呼び出しで定義されたアクセス許可セットのメタデータ署名の機能を設定または更新します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetPermissionSetProps (
    [in]  mdToken         tk,
    [in]  DWORD           dwAction,
    [in]  void const      *pvPermission,
    [in]  ULONG           cbPermission,
    [out] mdPermission    *ppm
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `tk`  
 から修飾されるオブジェクトを表すメタデータトークン。  
  
 `dwAction`  
 から使用する宣言セキュリティの種類を指定する[CorDeclSecurity](cordeclsecurity-enumeration.md)値です。  
  
 `pvPermission`  
 からアクセス許可 BLOB。  
  
 `cbPermission`  
 からのサイズ (バイト単位) `pvPermission` 。  
  
 `ppm`  
 入出力`mdPermission`更新されたアクセス許可を表すメタデータトークン。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IMetaDataEmit インターフェイス](imetadataemit-interface.md)
- [IMetaDataEmit2 インターフェイス](imetadataemit2-interface.md)
