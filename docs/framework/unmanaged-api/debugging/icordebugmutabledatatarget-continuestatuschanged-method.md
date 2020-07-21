---
title: ICorDebugMutableDataTarget::ContinueStatusChanged メソッド
ms.date: 03/30/2017
ms.assetid: 5a66d3f4-dd16-4d62-9dcc-0eab7041d894
ms.openlocfilehash: 49f517c0c09771ce86e43b801f6d7fce695d907a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213310"
---
# <a name="icordebugmutabledatatargetcontinuestatuschanged-method"></a>ICorDebugMutableDataTarget::ContinueStatusChanged メソッド
指定されたスレッド上の未処理のデバッグ イベントの継続状態を変更します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ContinueStatusChanged(  
   [in] DWORD dwThreadId,  
   [in] CORDB_CONTINUE_STATUS continueStatus);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwThreadId`  
 オペレーティング システム定義のスレッド識別子です。  
  
 `continueStatus`  
 新たに要求された継続状態を表す [COREDB_CONTINUE_STATUS](../common-data-types-unmanaged-api-reference.md) 値。  
  
## <a name="remarks"></a>Remarks  
 デバッガーは、通常の方法とは異なることがある方法で現在のデバッグ イベントを処理するように要求する ICorDebug メソッドを呼び出すときに、`ContinueStatusChanged` メソッドを呼び出します。 たとえば、未処理の例外が発生して、デバッガーが例外をキャンセルする操作 ([ICorDebugILFrame::SetIP](icordebugilframe-setip-method.md) または `FuncEval` など) を要求する場合、この API は例外のキャンセルを要求するために使用されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugMutableDataTarget インターフェイス](icordebugmutabledatatarget-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
