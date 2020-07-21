---
title: ICorDebugExceptionDebugEvent::GetStackPointer メソッド
ms.date: 03/30/2017
ms.assetid: d8f66a1c-16be-4264-afc5-bc2dfbb4a682
ms.openlocfilehash: 4f84183dfc23ebc0d0fee9feeb21329c217b9cca
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976019"
---
# <a name="icordebugexceptiondebugeventgetstackpointer-method"></a>ICorDebugExceptionDebugEvent::GetStackPointer メソッド
この例外デバッグ イベントのスタック ポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetStackPointer(  
   [out]CORDB_ADDRESS *pStackPointer  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pStackPointer`  
 [out] この例外デバッグ イベントのスタック ポインターのアドレスへのポインター。 詳細については、「解説」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 このスタック ポインターの意味は、次の表に示すように、イベントの種類によって異なります。  
  
|イベントの種類|`pStackPointer` 値の意味|  
|----------------|--------------------------------------|  
|[MANAGED_EXCEPTION_FIRST_CHANCE](cordebugrecordformat-enumeration.md)|例外をスローしたフレームのスタック ポインター。|  
|[MANAGED_EXCEPTION_USER_FIRST_CHANCE](cordebugrecordformat-enumeration.md)|スローされた例外の位置に最も近いユーザー コード フレームのスタック ポインター。|  
|[MANAGED_EXCEPTION_CATCH_HANDLER_FOUND](cordebugrecordformat-enumeration.md)|catch ハンドラーを含むフレームのスタック ポインター。|  
|[MANAGED_EXCEPTION_UNHANDLED](cordebugrecordformat-enumeration.md)|`pStackPointer` が **null** です。|  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
 イベントの種類は、[テキスト形式の[イベント:: GetEventKind](icordebugdebugevent-geteventkind-method.md)メソッドから取得できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugExceptionDebugEvent インターフェイス](icordebugexceptiondebugevent-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
