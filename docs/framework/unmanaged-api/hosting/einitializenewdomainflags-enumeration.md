---
title: EInitializeNewDomainFlags 列挙体
ms.date: 03/30/2017
api_name:
- EInitializeNewDomainFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EInitializeNewDomainFlags
helpviewer_keywords:
- EInitializeNewDomainFlags enumeration [.NET Framework hosting]
ms.assetid: 3a120ab2-f5ef-4c9b-8595-d3ed7247c342
ms.openlocfilehash: 7ff10f84d8d270d31c5d560fb3c9bd3c81cf3e24
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616230"
---
# <a name="einitializenewdomainflags-enumeration"></a>EInitializeNewDomainFlags 列挙体
ホストがアプリケーションドメインの初期化に関する情報をランタイムに提供できるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    eInitializeNewDomainFlags_None              = 0x0000,  
    eInitializeNewDomainFlags_NoSecurityChanges = 0x0002  
} EInitializeNewDomainFlags;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`eInitializeNewDomainFlags_None`|フラグなし。|  
|`eInitializeNewDomainFlags_NoSecurityChanges`|ホストがメソッド内のアプリケーションドメインのセキュリティ状態に変更を加えないことを、共通言語ランタイム (CLR) に通知し <xref:System.AppDomainManager.InitializeNewDomain%2A> ます。|  
  
## <a name="remarks"></a>解説  
 [ICLRDomainManager:: SetAppDomainManagerType](iclrdomainmanager-setappdomainmanagertype-method.md)メソッドは、型のパラメーターを受け取り `EInitializeNewDomainFlags` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスティングの列挙体](hosting-enumerations.md)
- [SetAppDomainManagerType メソッド](iclrdomainmanager-setappdomainmanagertype-method.md)
