---
title: ICorDebugEval::NewString メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugEval.NewString
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::NewString
helpviewer_keywords:
- NewString method [.NET Framework debugging]
- ICorDebugEval::NewString method [.NET Framework debugging]
ms.assetid: 29e7a14b-d50e-4852-bfda-011b76c0c9ee
topic_type:
- apiref
ms.openlocfilehash: b263fed7db5cb2ef687da45f8cbc99a02e1e3ea2
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976136"
---
# <a name="icordebugevalnewstring-method"></a>ICorDebugEval::NewString メソッド
指定された内容を持つ新しい文字列インスタンスを割り当てます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT NewString (  
    [in] LPCWSTR   string  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `string`  
 から文字列のコンテンツへのポインター。  
  
## <a name="remarks"></a>Remarks  
 文字列は常に、スレッドが現在実行されているアプリケーションドメインで作成されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
