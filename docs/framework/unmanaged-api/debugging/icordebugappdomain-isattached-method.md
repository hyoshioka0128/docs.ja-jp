---
title: ICorDebugAppDomain::IsAttached メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.IsAttached
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::IsAttached
helpviewer_keywords:
- IsAttached method [.NET Framework debugging]
- ICorDebugAppDomain::IsAttached method [.NET Framework debugging]
ms.assetid: af0c67c7-f53e-47c9-b84b-be50bd04903e
topic_type:
- apiref
ms.openlocfilehash: a2f6df7647ffe9f2adff963b6629ed29ece053c0
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895158"
---
# <a name="icordebugappdomainisattached-method"></a>ICorDebugAppDomain::IsAttached メソッド
デバッガーがアプリケーションドメインにアタッチされているかどうかを示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsAttached (  
    [out] BOOL  *pbAttached  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbAttached`  
 入出力`true`デバッガーがアプリケーションドメインにアタッチされている場合は。それ以外`false`の場合は。  
  
## <a name="remarks"></a>解説  
 このデバッガーがアプリケーションドメインにアタッチされるまでは、このコントロールメソッドを使用できません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
