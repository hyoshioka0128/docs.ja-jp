---
title: ICorDebugProcess::GetHandle メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetHandle
helpviewer_keywords:
- GetHandle method, ICorDebugProcess interface [.NET Framework debugging]
- ICorDebugProcess::GetHandle method [.NET Framework debugging]
ms.assetid: e7d3ecf5-09d2-4d94-abb6-ff3483deebb6
topic_type:
- apiref
ms.openlocfilehash: ed7110cb2e2b7a91ed81d2d81c2989d1733c1ee6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207313"
---
# <a name="icordebugprocessgethandle-method"></a>ICorDebugProcess::GetHandle メソッド
プロセスを処理するハンドルを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetHandle([out] HPROCESS *phProcessHandle);  
```  
  
## <a name="parameters"></a>パラメーター  
 `phProcessHandle`  
 入出力プロセスを指すハンドルであるへのポインター `HPROCESS` 。  
  
## <a name="remarks"></a>Remarks  
 取得したハンドルは、デバッグインターフェイスによって所有されています。 デバッガーは、使用する前にハンドルを複製する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
