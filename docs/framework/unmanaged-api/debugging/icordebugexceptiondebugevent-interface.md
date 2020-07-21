---
title: ICorDebugExceptionDebugEvent インターフェイス
ms.date: 03/30/2017
ms.assetid: f9ba60d8-b54d-417e-bb3e-fde4b41ca44c
ms.openlocfilehash: dfa65aa1b63c996068e75ff1165111d5fcfe77eb
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976006"
---
# <a name="icordebugexceptiondebugevent-interface"></a>ICorDebugExceptionDebugEvent インターフェイス
は、例外イベントをサポートするために、の[イベント](icordebugdebugevent-interface.md)インターフェイスを拡張します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetFlags メソッド](icordebugexceptiondebugevent-getflags-method.md)|例外をインターセプトできるかどうかを示すフラグを取得します。|  
|[GetNativeIP メソッド](icordebugexceptiondebugevent-getnativeip-method.md)|この例外デバッグ イベントのネイティブ インターフェイス ポインターを取得します。|  
|[GetStackPointer メソッド](icordebugexceptiondebugevent-getstackpointer-method.md)|この例外デバッグ イベントのスタック ポインターを取得します。|  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugExceptionDebugEvent` インターフェイスは、次のイベントの種類によって実装されます。  
  
- [MANAGED_EXCEPTION_FIRST_CHANCE](cordebugrecordformat-enumeration.md)  
  
- [MANAGED_EXCEPTION_USER_FIRST_CHANCE](cordebugrecordformat-enumeration.md)  
  
- [MANAGED_EXCEPTION_CATCH_HANDLER_FOUND](cordebugrecordformat-enumeration.md)  
  
- [MANAGED_EXCEPTION_UNHANDLED](cordebugrecordformat-enumeration.md)  
  
> [!NOTE]
> このインターフェイスは .NET ネイティブでのみ使用可能です。 インターフェイス ポインターを取得するために `QueryInterface` を呼び出そうとすると、.NET ネイティブ外の ICorDebug シナリオに対して `E_NOINTERFACE` が返されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
