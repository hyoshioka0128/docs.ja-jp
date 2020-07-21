---
title: DestroyICeeFileGen 関数
ms.date: 03/30/2017
api_name:
- DestroyICeeFileGen
api_location:
- mscoree.dll
- mscorpehost.dll
- mscorpe.dll
api_type:
- COM
f1_keywords:
- DestroyICeeFileGen
helpviewer_keywords:
- DestroyICeeFileGen function [.NET Framework hosting]
ms.assetid: dc1e2235-e721-4cb2-a0b8-6b0c030d7bab
topic_type:
- apiref
ms.openlocfilehash: ff7e7b299d185b8db263d2076c1e075b87b487fc
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616399"
---
# <a name="destroyiceefilegen-function"></a>DestroyICeeFileGen 関数
[ICeeFileGen](iceefilegen-class.md)オブジェクトを破棄します。  
  
 この関数は .NET Framework 4 で非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DestroyICeeFileGen (  
    [in] ICeeFileGen  **ceeFileGen  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ceeFileGen`  
 から`ICeeFileGen`破棄するオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、標準の COM エラーコードを返します。  
  
## <a name="remarks"></a>解説  
 `DestroyICeeFileGen``ICeeFileGen` [CreateICeeFileGen](createiceefilegen-function.md)関数によって作成されたオブジェクトを破棄します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** ICeeFileGen  
  
 **ライブラリ:** MSCorPE  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
