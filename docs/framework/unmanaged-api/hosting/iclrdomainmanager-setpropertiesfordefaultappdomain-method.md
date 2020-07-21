---
title: ICLRDomainManager::SetPropertiesForDefaultAppDomain メソッド
ms.date: 03/30/2017
api_name:
- ICLRDomainManager.SetPropertiesForDefaultAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager::SetPropertiesForDefaultAppDomain
helpviewer_keywords:
- ICLRDomainManager::SetPropertiesForDefaultAppDomain method [.NET Framework hosting]
- SetPropertiesForDefaultAppDomain method [.NET Framework hosting]
ms.assetid: 43e61c4b-c435-45ec-9ef6-c68403aa4200
ms.openlocfilehash: 5e1c1b1984c63bedb3c073f45a7b9a3574afdcec
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615684"
---
# <a name="iclrdomainmanagersetpropertiesfordefaultappdomain-method"></a>ICLRDomainManager::SetPropertiesForDefaultAppDomain メソッド
既定のアプリケーションドメインを初期化するために使用されるプロパティを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetPropertiesForDefaultAppDomain(  
    [in] DWORD nProperties,  
    [in] LPCWSTR *pwszPropertyNames,  
    [in] LPCWSTR *pwszPropertyValues  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `nProperties`  
 からとのエントリの数 `pwszPropertyNames` `pwszPropertyValues` 。  
  
 `pwszPropertyNames`  
 からプロパティ名の配列。プロパティがない場合は null。 現時点では、このメソッドによって認識される唯一のプロパティ名は "PARTIAL_TRUST_VISIBLE_ASSEMBLIES" です。  
  
 `pwszPropertyValues`  
 からプロパティ値の配列。プロパティがない場合は null。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|HRESULT_FROM_WIN32 (ERROR_UNKNOWN_PROPERTY)|`pwszPropertyNames`には、このメソッドで認識されないプロパティ名が含まれています。|  
  
## <a name="remarks"></a>解説  
 "PARTIAL_TRUST_VISIBLE_ASSEMBLIES" のプロパティ値は、条件付き (APTCA) 属性を持つアセンブリのリストです。このフラグは、 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> <xref:System.Security.PartialTrustVisibilityLevel.NotVisibleByDefault?displayProperty=nameWithType> 既定のアプリケーションドメインの部分的に信頼された呼び出し元に対して表示されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスティング](index.md)
- [ICLRDomainManager インターフェイス](iclrdomainmanager-interface.md)
