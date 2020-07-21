---
title: EContextType 列挙型
ms.date: 03/30/2017
api_name:
- EContextType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EContextType
helpviewer_keywords:
- EContextType enumeration [.NET Framework hosting]
ms.assetid: 92b926a9-b87e-408a-9036-df7b752c9492
topic_type:
- apiref
ms.openlocfilehash: b93b27957cc715a5b4718dd9ef61cd11f4a39914
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84493418"
---
# <a name="econtexttype-enumeration"></a>EContextType 列挙型
現在実行中のスレッドのセキュリティコンテキストを記述します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    eCurrentContext    = 0x00,  
    eRestrictedContext = 0x01  
} EContextType;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`eCurrentContext`|共通言語ランタイム (CLR) が[IHostSecurityManager:: GetSecurityContext](ihostsecuritymanager-getsecuritycontext-method.md)メソッドを呼び出す時点での現在のスレッドのコンテキスト、または[IHostSecurityManager:: SetSecurityContext](ihostsecuritymanager-setsecuritycontext-method.md)メソッドの呼び出しで CLR によって要求されたコンテキストを示します。|  
|`eRestrictedContext`|ホストが低い特権 (ガベージコレクター、クラスまたはモジュールコンストラクターなど) を持つコンテキストを示します。|  
  
## <a name="remarks"></a>解説  
 CLR は、 `EContextType` メソッドとメソッドの呼び出しで、値の1つをパラメーター値として提供し `IHostSecurityManager::GetSecurityContext` `IHostSecurityManager::SetSecurityContext` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IHostSecurityContext インターフェイス](ihostsecuritycontext-interface.md)
- [IHostSecurityManager インターフェイス](ihostsecuritymanager-interface.md)
- [ホスティングの列挙型](hosting-enumerations.md)
