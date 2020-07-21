---
title: IMetaDataImport::GetPermissionSetProps メソッド
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetPermissionSetProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetPermissionSetProps
helpviewer_keywords:
- GetPermissionSetProps method [.NET Framework metadata]
- IMetaDataImport::GetPermissionSetProps method [.NET Framework metadata]
ms.assetid: 9855f0e4-12c0-4d3d-ab5d-d6bc52d25eae
topic_type:
- apiref
ms.openlocfilehash: 54c75156c32e5b40aa933ef6530b2cc33edf7de4
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84490992"
---
# <a name="imetadataimportgetpermissionsetprops-method"></a>IMetaDataImport::GetPermissionSetProps メソッド
指定した <xref:System.Security.PermissionSet?displayProperty=nameWithType> アクセス許可トークンによって表されるに関連付けられているメタデータを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetPermissionSetProps (  
   [in]  mdPermission      pm,  
   [out] DWORD             *pdwAction,
   [out] void const        **ppvPermission,
   [out] ULONG             *pcbPermission  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pm`  
 からメタデータプロパティを取得するアクセス許可セットを表すアクセス許可メタデータトークン。  
  
 `pdwAction`  
 入出力アクセス許可セットへのポインター。  
  
 `ppvPermission`  
 入出力アクセス許可セットのバイナリメタデータシグネチャへのポインター。  
  
 `pcbPermission`  
 入出力のサイズ (バイト単位) `ppvPermission` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Security.PermissionSet>
- [IMetaDataImport インターフェイス](imetadataimport-interface.md)
- [IMetaDataImport2 インターフェイス](imetadataimport2-interface.md)
