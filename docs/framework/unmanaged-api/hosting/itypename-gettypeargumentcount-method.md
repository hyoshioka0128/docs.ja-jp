---
title: ITypeName::GetTypeArgumentCount メソッド
ms.date: 03/30/2017
api_name:
- ITypeName.GetTypeArgumentCount
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- GetTypeArgumentCount
helpviewer_keywords:
- GetTypeArgumentCount method [.NET Framework hosting]
- ITypeName::GetTypeArgumentCount method [.NET Framework hosting]
ms.assetid: ecb5480c-761a-4b02-83e0-b79abc67fd08
topic_type:
- apiref
ms.openlocfilehash: 627e4f596cde8f02edcaecfb26fa277b5ecf3a6b
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842141"
---
# <a name="itypenamegettypeargumentcount-method"></a>ITypeName::GetTypeArgumentCount メソッド
このメソッドは、.NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTypeArgumentCount (  
    [out, retval] DWORD* pCount  
);  
```  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト インターフェイス](hosting-interfaces.md)
