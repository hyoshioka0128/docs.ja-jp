---
title: ICorDebugHeapEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugHeapEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapEnum::Next
helpviewer_keywords:
- ICorDebugHeapEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugHeapEnum interface [.NET Framework debugging]
ms.assetid: 2221fd06-9e27-4113-972e-2530db8c3594
topic_type:
- apiref
ms.openlocfilehash: 5d0b231b4014e60a9e8778c6b9d6ed7758b2d8c5
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83208474"
---
# <a name="icordebugheapenumnext-method"></a>ICorDebugHeapEnum::Next メソッド
マネージヒープ上のオブジェクトに関する情報を格納している、指定した数の[COR_HEAPOBJECT](cor-heapobject-structure.md)インスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next(  
    [in] ULONG celt,    [out, size_is(celt), length_is(*pceltFetched)] COR_HEAPOBJECT  objects[],
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 celt  
 [in] 取得するオブジェクトの数。  
  
 オブジェクト  
 入出力ポインターの配列。各ポインターは、マネージヒープ上のオブジェクトに関する情報を提供する[COR_HEAPOBJECT](cor-heapobject-structure.md)オブジェクトを指します。  
  
 pceltFetched  
 入出力実際にで返される[COR_HEAPOBJECT](cor-heapobject-structure.md)オブジェクトの数へのポインター `objects` 。 `celt` が 1 の場合、この値は`null` になることがあります。  
  
## <a name="remarks"></a>Remarks  
 `COR_HEAPOBJECT.type` フィールドは、入れ子になった参照カウントの COM インターフェイスの識別子です。 この参照は、`ICorDebugHeapEnum::Next` の呼び出し元によって解放される必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugHeapEnum インターフェイス](icordebugheapenum-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
