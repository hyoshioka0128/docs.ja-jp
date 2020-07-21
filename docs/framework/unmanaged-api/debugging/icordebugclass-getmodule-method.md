---
title: ICorDebugClass::GetModule メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugClass.GetModule
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass::GetModule
helpviewer_keywords:
- GetModule method, ICorDebugClass interface [.NET Framework debugging]
- ICorDebugClass::GetModule method [.NET Framework debugging]
ms.assetid: 87029cc4-e5e1-42d5-8b98-655bb7ece520
topic_type:
- apiref
ms.openlocfilehash: fd048b692ad05f60621a057024be22cb48b3abbe
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894197"
---
# <a name="icordebugclassgetmodule-method"></a>ICorDebugClass::GetModule メソッド
このクラスを定義するモジュールを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetModule (  
    [out] ICorDebugModule    **pModule  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pModule`  
 入出力このクラスが定義されているモジュールを表す、モジュールオブジェクトのアドレスへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
