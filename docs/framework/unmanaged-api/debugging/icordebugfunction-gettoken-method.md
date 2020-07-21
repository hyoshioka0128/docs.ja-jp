---
title: ICorDebugFunction::GetToken メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetToken
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetToken
helpviewer_keywords:
- ICorDebugFunction::GetToken method [.NET Framework debugging]
- GetToken method, ICorDebugFunction interface [.NET Framework debugging]
ms.assetid: c6bbf479-062e-48e9-9c70-0f92e293e36a
topic_type:
- apiref
ms.openlocfilehash: e542145e888049231a6c5e4cccbb4ee96c62f98b
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213258"
---
# <a name="icordebugfunctiongettoken-method"></a>ICorDebugFunction::GetToken メソッド
この関数のメタデータトークンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetToken (  
    [out] mdMethodDef *pMethodDef  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pMethodDef`  
 入出力`mdMethodDef`この関数のメタデータを参照するトークンへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
