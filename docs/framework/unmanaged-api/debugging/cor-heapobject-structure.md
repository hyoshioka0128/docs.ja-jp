---
title: COR_HEAPOBJECT 構造体
ms.date: 03/30/2017
api_name:
- COR_HEAPOBJECT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_HEAPOBJECT
helpviewer_keywords:
- COR_HEAPOBJECT structure [.NET Framework debugging]
ms.assetid: a92fdf95-492b-49ae-a741-2186e5c1d7c5
topic_type:
- apiref
ms.openlocfilehash: efb3d913e1d8ef0c486d7e5e1d9777ae7d88bc71
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179333"
---
# <a name="cor_heapobject-structure"></a>COR_HEAPOBJECT 構造体
マネージド ヒープ上のオブジェクトに関する情報が提供されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _COR_HEAPOBJECT {  
    CORDB_ADDRESS address;
    ULONG64 size;
    COR_TYPEID type;
} COR_HEAPOBJECT;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`address`|メモリ内のオブジェクトのアドレス。|  
|`size`|オブジェクトの合計サイズ (バイト単位)。|  
|`type`|オブジェクトの型を表す[COR_TYPEID](cor-typeid-structure.md)トークン。|  
  
## <a name="remarks"></a>解説  
 `COR_HEAPOBJECT`インスタンスは、メソッドを呼び出すことによって設定される[ICorDebugHeapEnum](icordebugheapenum-interface.md)インターフェイス オブジェクトを列挙することによって取得[ICorDebugProcess5::EnumerateHeap](icordebugprocess5-enumerateheap-method.md)できます。  
  
 インスタンス`COR_HEAPOBJECT`は、マネージ ヒープ上のライブ オブジェクトに関する情報、またはオブジェクトによってルートされていないが、まだガベージ コレクターによって収集されていないオブジェクトに関する情報を提供します。  
  
 パフォーマンスを`COR_HEAPOBJECT.address`向上させるには、このフィールドは`CORDB_ADDRESS`、デバッグ API の多くで使用される ICorDebugValue インターフェイス値ではなく値です。 特定のオブジェクト アドレスのオブジェクトを取得するには、値を`CORDB_ADDRESS` [ICorDebugProcess5::GetObject](icordebugprocess5-getobject-method.md)メソッドに渡します。  
  
 パフォーマンスを`COR_HEAPOBJECT.type`向上させるには、このフィールドは`COR_TYPEID`、デバッグ API の多くで使用される ICorDebugType インターフェイス値ではなく値です。 特定の型 ID のオブジェクトを取得するには、`COR_TYPEID`値を[ICorDebugProcess5::GetTypeForTypeID](icordebugprocess5-gettypefortypeid-method.md)メソッドに渡します。  
  
 構造体`COR_HEAPOBJECT`には、参照カウントされる COM インターフェイスが含まれています。 列挙子からインスタンス`COR_HEAPOBJECT`を取得する場合は、呼び出すことによって、 [ICorDebugHeapEnum::Next](icordebugheapenum-next-method.md)メソッド、後で参照を解放する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
