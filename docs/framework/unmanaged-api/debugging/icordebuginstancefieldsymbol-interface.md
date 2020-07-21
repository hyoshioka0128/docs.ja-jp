---
title: ICorDebugInstanceFieldSymbol インターフェイス
ms.date: 03/30/2017
ms.assetid: a4a8f259-b83a-4425-ae8b-72b067dbc0d9
ms.openlocfilehash: 092f2a8acdffa9f91176bdf0ca10b8db9cff6d37
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209930"
---
# <a name="icordebuginstancefieldsymbol-interface"></a>ICorDebugInstanceFieldSymbol インターフェイス
インスタンス フィールドのデバッグ シンボル情報を表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetName メソッド](icordebuginstancefieldsymbol-getname-method.md)|インスタンス フィールドの名前を取得します。|  
|[GetOffset メソッド](icordebuginstancefieldsymbol-getoffset-method.md)|このインスタンス フィールドの親クラスにおける、このインスタンス フィールドのオフセット (バイト単位) を取得します。|  
|[GetSize メソッド](icordebuginstancefieldsymbol-getsize-method.md)|インスタンス フィールドのサイズ (バイト単位) を取得します。|  
  
## <a name="remarks"></a>Remarks  
 `ICorDebugInstanceFieldSymbol` インターフェイスは、インスタンス フィールドのデバッグ シンボル情報を取得するために使用されます。  
  
> [!NOTE]
> このインターフェイスは .NET ネイティブでのみ使用可能です。 .NET ネイティブの外部で ICorDebug シナリオについてこのインターフェイスを実装する場合は、共通言語ランタイムはこのインターフェイスを無視します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugStaticFieldSymbol インターフェイス](icordebugstaticfieldsymbol-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
