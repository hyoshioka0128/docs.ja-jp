---
title: ICorDebugAppDomain4::GetObjectForCCW メソッド
ms.date: 03/30/2017
ms.assetid: 2cacdb85-e7b8-42e7-b310-c3e8c22e5d33
ms.openlocfilehash: a175a6b6c91c284348580e1d9dc9ef0c5f5fc5df
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895117"
---
# <a name="icordebugappdomain4getobjectforccw-method"></a>ICorDebugAppDomain4::GetObjectForCCW メソッド
COM 呼び出し可能ラッパー (CCW: COM Callable Wrapper) ポインターからマネージド オブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetObjectForCCW(  
   [in]CORDB_ADDRESS ccwPointer,
   [out]ICorDebugValue **ppManagedObject  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ccwPointer`  
 [in] COM 呼び出し可能ラッパー (CCW) ポインター。  
  
 `ppManagedObject`  
 入出力指定された CCW ポインターに対応するマネージオブジェクトを表す "ICorDebugValue" オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugAppDomain4 インターフェイス](icordebugappdomain4-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
