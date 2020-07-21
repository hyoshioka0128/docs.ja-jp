---
title: ICorDebugMDA::GetFlags メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugMDA.GetFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA::GetFlags
helpviewer_keywords:
- ICorDebugMDA::GetFlags method [.NET Framework debugging]
- GetFlags method [.NET Framework debugging]
ms.assetid: 87ce7c5b-fd82-453e-bf55-c8a32150b183
topic_type:
- apiref
ms.openlocfilehash: 4e5939e9e74899a33f28927c4fda09d0a8fb30a0
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209735"
---
# <a name="icordebugmdagetflags-method"></a>ICorDebugMDA::GetFlags メソッド
によって表されるマネージデバッグアシスタント (MDA) に関連付けら[れている](icordebugmda-interface.md)フラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFlags (  
    [in] CorDebugMDAFlags *pFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pFlags`  
 からこの MDA のフラグの設定を指定する[Cordebugmdaflags](cordebugmdaflags-enumeration.md)列挙値のビットごとの組み合わせ。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugMDA インターフェイス](icordebugmda-interface.md)
- [マネージド デバッグ アシスタントによるエラーの診断](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
