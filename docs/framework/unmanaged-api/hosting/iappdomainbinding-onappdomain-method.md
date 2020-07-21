---
title: IAppDomainBinding::OnAppDomain メソッド
ms.date: 03/30/2017
api_name:
- IAppDomainBinding.OnAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- OnAppDomain
helpviewer_keywords:
- IAppDomainBinding::OnAppDomain method [.NET Framework hosting]
- OnAppDomain method [.NET Framework hosting]
ms.assetid: b419dcc9-e8aa-484b-af0d-0f40358edb99
topic_type:
- apiref
ms.openlocfilehash: 2d5dbd003d0ea5decae0025d47e6bd5c1fb1ed4a
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83617075"
---
# <a name="iappdomainbindingonappdomain-method"></a>IAppDomainBinding::OnAppDomain メソッド
アプリケーションドメインが作成されたことをホストに通知するために、共通言語ランタイム (CLR) によって呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OnAppDomain (  
    [in] IUnknown* pAppdomain  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppdomain`  
 から新しいアプリケーションドメインを表す[IUnknown](/cpp/atl/iunknown)インターフェイスオブジェクトへのポインター。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IAppDomainBinding インターフェイス](iappdomainbinding-interface.md)
