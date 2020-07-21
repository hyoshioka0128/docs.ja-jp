---
title: ICorDebugProcess::EnumerateAppDomains メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.EnumerateAppDomains
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::EnumerateAppDomains
helpviewer_keywords:
- ICorDebugProcess::EnumerateAppDomains method [.NET Framework debugging]
- EnumerateAppDomains method [.NET Framework debugging]
ms.assetid: d508981f-e2b2-445b-a649-69951c22702d
topic_type:
- apiref
ms.openlocfilehash: 748a44075f7f73e54bab689bcb8865dee2b14946
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207837"
---
# <a name="icordebugprocessenumerateappdomains-method"></a>ICorDebugProcess::EnumerateAppDomains メソッド
このプロセス内のすべてのアプリケーションドメインを列挙します。  
  
## <a name="syntax"></a>構文  
  
``` cpp
HRESULT EnumerateAppDomains(  
    [out] ICorDebugAppDomainEnum **ppAppDomains);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppAppDomains`  
 入出力このプロセス内のアプリケーションドメインの列挙子である[ICorDebugAppDomainEnum](icordebugappdomainenum-interface.md)のアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 このメソッド[は、によって](icordebugmanagedcallback-createprocess-method.md)使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
