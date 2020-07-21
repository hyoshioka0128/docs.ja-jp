---
title: ICLRDomainManager インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRDomainManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager
helpviewer_keywords:
- ICLRDomainManager interface [.NET Framework hosting]
ms.assetid: f08b2390-d872-4521-a815-e9c237c4c45d
ms.openlocfilehash: dda243ccbf18f396c1bcc03358997ea0f06c42a8
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615710"
---
# <a name="iclrdomainmanager-interface"></a>ICLRDomainManager インターフェイス
既定のアプリケーションドメインを初期化し、初期化プロパティを指定するために使用されるアプリケーションドメインマネージャーをホストが指定できるようにします。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[SetAppDomainManagerType メソッド](iclrdomainmanager-setappdomainmanagertype-method.md)|<xref:System.AppDomainManager?displayProperty=nameWithType>既定のアプリケーションドメインを初期化するために使用されるアプリケーションドメインマネージャーのクラスから派生した型を指定します。|  
|[SetPropertiesForDefaultAppDomain メソッド](iclrdomainmanager-setpropertiesfordefaultappdomain-method.md)|既定のアプリケーションドメインを初期化するために使用されるプロパティを設定します。|  
  
## <a name="remarks"></a>解説  
 このインターフェイスのインスタンスを取得するには、マネージャーの型 IID で[ICLRControl:: GetCLRManager](iclrcontrol-getclrmanager-method.md)メソッドを呼び出し `IID_ICLRDomainManager` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト インターフェイス](hosting-interfaces.md)
- [ホスティング](index.md)
