---
title: ICorDebugStackWalk::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk.Next Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk::Next
helpviewer_keywords:
- ICorDebugStackWalk::Next method [.NET Framework debugging]
- Next method, ICorDebugStackWalk interface [.NET Framework debugging]
ms.assetid: 189c36be-028c-4fba-a002-5edfb8fcd07f
topic_type:
- apiref
ms.openlocfilehash: b89e968e9b12943c8192af3b280f8bd321a02110
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378792"
---
# <a name="icordebugstackwalknext-method"></a>ICorDebugStackWalk::Next メソッド
このオブジェクトを次のフレームに[移動します](icordebugstackwalk-interface.md)。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next();  
```  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|ランタイムが次のフレームに正常にアンワインドされました (「解説」を参照してください)。|  
|E_FAIL|`ICorDebugStackWalk`オブジェクトを拡張できませんでした。|  
|CORDBG_S_AT_END_OF_STACK|このアンワインドの結果、スタックの末尾に到達しました。|  
|CORDBG_E_PAST_END_OF_STACK|フレームポインターは既にスタックの末尾にあります。そのため、追加のフレームにアクセスすることはできません。|  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>Remarks  
 メソッドは、 `Next` `ICorDebugStackWalk` ランタイムが現在のフレームをアンワインドできる場合にのみ、オブジェクトを呼び出し元のフレームに進めます。 それ以外の場合、オブジェクトは、ランタイムがアンワインドできる次のフレームに進みます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugStackWalk インターフェイス](icordebugstackwalk-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
