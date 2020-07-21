---
title: ICorDebugInstanceFieldSymbol::GetOffset メソッド
ms.date: 03/30/2017
ms.assetid: 7e470150-2b92-4425-989c-315f48964fd2
ms.openlocfilehash: 7d553c1a446e06f34c20da18c0edfe6773cfb597
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209982"
---
# <a name="icordebuginstancefieldsymbolgetoffset-method"></a>ICorDebugInstanceFieldSymbol::GetOffset メソッド
このインスタンス フィールドの親クラスにおける、このインスタンス フィールドのオフセット (バイト単位) を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetOffset(  
   [out] ULONG32 *pcbOffset  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pcbOffset`  
 このインスタンス フィールドの親クラスにおける、このフィールドのオフセットのバイト数へのポインター。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugInstanceFieldSymbol インターフェイス](icordebuginstancefieldsymbol-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
