---
title: ICorDebugBlockingObjectEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugBlockingObjectEnum.Next Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBlockingObjectEnum::Next
helpviewer_keywords:
- Next method, ICorDebugBlockingObjectEnum interface [.NET Framework debugging]
- ICorDebugBlockingObjectEnum::Next method [.NET Framework debugging]
ms.assetid: 0121753f-ebea-48d0-aeb2-ed7fda76dc60
topic_type:
- apiref
ms.openlocfilehash: 0ef49d2d833841eac62b2b964a0fdc902b4fb6a9
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894769"
---
# <a name="icordebugblockingobjectenumnext-method"></a>ICorDebugBlockingObjectEnum::Next メソッド
現在の位置から開始して、指定した数の[CorDebugBlockingObject](cordebugblockingobject-structure.md)オブジェクトを列挙から取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next([in] ULONG  celt,  
             [out, size_is(celt), length_is(*pceltFetched)]  
                           CorDebugBlockingObject values[],  
             [out] ULONG *pceltFetched;  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 から取得するオブジェクトの数。  
  
 `values`  
 入出力[CorDebugBlockingObject](cordebugblockingobject-structure.md)オブジェクトへのポインターの配列。  
  
 `pceltFetched`  
 入出力取得されたオブジェクトの数へのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT を返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|S_FALSE|`pceltFetched` は `celt` と一致しません。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、一般的な COM 列挙子と同様に機能します。  
  
 入力配列の値は、少なくともサイズ`celt`にする必要があります。 配列には、列挙体の次`celt`の値、または残りのすべての値`celt`を格納します。 このメソッドから制御が`pceltFetched`戻るときに、取得された値の数がに格納されます。 に`values`無効なポインターが含まれている場合、または`celt`より小さいバッファー `pceltFetched`を指している場合、またはが無効なポインターの場合、結果は未定義になります。  
  
> [!NOTE]
> [CorDebugBlockingObject](cordebugblockingobject-structure.md)構造体を解放する必要はありませんが、その中の "ICorDebugValue" インターフェイスは解放する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugDataTarget インターフェイス](icordebugdatatarget-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
