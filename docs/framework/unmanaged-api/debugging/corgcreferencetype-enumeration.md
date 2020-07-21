---
title: CorGCReferenceType 列挙型
ms.date: 03/30/2017
api_name:
- CorGCReferenceType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorGCReferenceType
helpviewer_keywords:
- CorGCReferenceType
ms.assetid: d9f16439-5a36-4474-8ffd-4f0b2c2bb686
topic_type:
- apiref
ms.openlocfilehash: d156f103c3812c91da380e722a1c6c95d621df4c
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860918"
---
# <a name="corgcreferencetype-enumeration"></a>CorGCReferenceType 列挙型
ガベージ コレクトされる必要のあるオブジェクトのソースを識別します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    CorHandleStrong = 1,  
    CorHandleStrongPinning = 2,  
    CorHandleWeakShort = 4,  
    CorHandleWeakRefCount = 8,  
    CorHandleStrongRefCount = 32,  
    CorHandleStrongDependent = 64,  
    CorHandleStrongAsyncPinned = 128,  
    CorHandleStrongSizedByref = 256,  
  
    CorReferenceStack = 0x80000001,  
    CorReferenceFinalizer = 0x80000002,  
  
    CorHandleStrongOnly = 0x1E3,  
    CorHandleWeakOnly = 0xC,  
    CorHandleAll = 0x7FFFFFFF  
} CorGCReferenceType  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー名|説明|  
|-----------------|-----------------|  
|`CorHandleStrong`|オブジェクト ハンドル テーブルからの強い参照へのハンドル。|  
|`CorHandleStrongPinning`|オブジェクトハンドルテーブルからの固定された強い参照へのハンドル。|  
|`CorHandleWeakShort`|オブジェクトハンドルテーブルからの弱い参照へのハンドル。|  
|`CorHandleWeakRefCount`|オブジェクトハンドルテーブルからの弱い参照カウントオブジェクトへのハンドル。|  
|`CorHandleStrongRefCount`|オブジェクトハンドルテーブルからの参照カウントオブジェクトへのハンドル。|  
|`CorHandleStrongDependent`|オブジェクトハンドルテーブルからの依存オブジェクトへのハンドル。|  
|`CorHandleStrongAsyncPinned`|オブジェクト ハンドル テーブルからの非同期固定オブジェクト。|  
|`CorHandleStrongSizedByref`|ガベージ コレクション時に、すべてのオブジェクトおよびオブジェクト ルートの集合的なクロージャの概算サイズを保持する強力なハンドル。|  
|`CorReferenceStack`|マネージスタックからの参照。|  
|`CorReferenceFinalizer`|ファイナライザーキューからの参照。|  
|CorHandleStrongOnly|ハンドルテーブルからの強い参照だけを返します。 この値は、 [ICorDebugProcess5:: EnumerateHandles](icordebugprocess5-enumeratehandles-method.md)メソッドによってのみ使用されます。|  
|`CorHandleWeakOnly`|ハンドルテーブルからの弱い参照だけを返します。 この値は、 [ICorDebugProcess5:: EnumerateHandles](icordebugprocess5-enumeratehandles-method.md)メソッドによってのみ使用されます。|  
|`CorHandleAll`|Handle テーブルからすべての参照を返します。 この値は、 [ICorDebugProcess5:: EnumerateHandles](icordebugprocess5-enumeratehandles-method.md)メソッドによってのみ使用されます。|  
  
## <a name="remarks"></a>解説  
 列挙`CorGCReferenceType`体は次のように使用されます。  
  
- `type` [COR_GC_REFERENCE](cor-gc-reference-structure.md)構造体のフィールドの値として、参照またはハンドルのソースを示します。  
  
- `types` [ICorDebugProcess5:: EnumerateHandles](icordebugprocess5-enumeratehandles-method.md)メソッドの引数として、列挙体に含めるハンドルの種類を指定します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のデバッグ](debugging-enumerations.md)
