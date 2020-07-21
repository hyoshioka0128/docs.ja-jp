---
title: ICorDebugProcess5::EnumerateHeapRegions メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHeapRegions
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHeapRegions
helpviewer_keywords:
- EnumerateHeapRegions method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeapRegions method [.NET Framework debugging]
ms.assetid: b1edba68-9c36-4f69-be9f-678ce0b33480
topic_type:
- apiref
ms.openlocfilehash: 50b0859d6727a25906f2c8b0f3fe96da228ab886
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213557"
---
# <a name="icordebugprocess5enumerateheapregions-method"></a>ICorDebugProcess5::EnumerateHeapRegions メソッド
マネージヒープのメモリ範囲の列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumerateHeapRegions(  
   [out] ICorDebugHeapSegmentEnum **ppRegions  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppRegions`  
 入出力マネージヒープ内にオブジェクトが格納されているメモリ範囲の列挙子である[ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md) interface オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 メソッドを呼び出す前に `ICorDebugProcess5::EnumerateHeapRegions` 、 [ICorDebugProcess5:: Getg](icordebugprocess5-getgcheapinformation-method.md)メソッドを呼び出し、 `areGCStructuresValid` 返された[COR_HEAPINFO](cor-heapinfo-structure.md)オブジェクトのフィールドの値を調べて、現在の状態のガベージコレクションヒープが列挙可能であることを確認する必要があります。 さらに、 `ICorDebugProcess5::EnumerateHeapRegions` `E_FAIL` メモリ領域が作成される前に、プロセスの有効期間が早すぎると、メソッドはを返します。  
  
 このメソッドは、マネージオブジェクトを含む可能性があるすべてのメモリ領域を列挙することが保証されていますが、それらの領域にマネージオブジェクトが実際に存在することは保証されません。 [ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md) collection オブジェクトには、空または予約済みのメモリ領域を含めることができます。  
  
 [ICorDebugHeapSegmentEnum](icordebugheapsegmentenum-interface.md)インターフェイスオブジェクトは、ICorDebugEnum インターフェイスから派生した標準列挙子であり、 [COR_SEGMENT](cor-segment-structure.md)オブジェクトを列挙できます。 各[COR_SEGMENT](cor-segment-structure.md)オブジェクトは、特定のセグメントのメモリ範囲に関する情報と、そのセグメント内のオブジェクトの生成を提供します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugProcess5 インターフェイス](icordebugprocess5-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
