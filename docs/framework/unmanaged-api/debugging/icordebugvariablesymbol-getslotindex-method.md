---
title: ICorDebugVariableSymbol::GetSlotIndex メソッド
ms.date: 03/30/2017
ms.assetid: 09c19f5f-afc4-4e0c-bffe-cd7147bc7a43
ms.openlocfilehash: 251a978e96ff396d0d9d9282ded7f8a25ae0ba0b
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83397091"
---
# <a name="icordebugvariablesymbolgetslotindex-method"></a>ICorDebugVariableSymbol::GetSlotIndex メソッド
ローカル変数のマネージド スロット インデックスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetSlotIndex(  
   [out] ULONG32 *pSlotIndex  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pSlotIndex`  
 [out] ローカル変数のスロット インデックスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 正常終了した場合は、`S_OK`。 変数が関数引数の場合は `E_FAIL`。  
  
## <a name="remarks"></a>解説  
 ローカル変数のマネージド スロット インデックスを使用すると、変数のメタデータ情報を取得できます。  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugVariableSymbol インターフェイス](icordebugvariablesymbol-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
