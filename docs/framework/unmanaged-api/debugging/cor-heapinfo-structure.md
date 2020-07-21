---
title: COR_HEAPINFO 構造体
ms.date: 03/30/2017
api_name:
- COR_HEAPINFO
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_HEAPINFO
helpviewer_keywords:
- COR_HEAPINFO structure [.NET Framework debugging]
ms.assetid: bfb2cd39-3e0b-4d51-ba0c-f009755c1456
topic_type:
- apiref
ms.openlocfilehash: 37659262695b63a6dd6390c62c4bb7e04fdadca4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179306"
---
# <a name="cor_heapinfo-structure"></a>COR_HEAPINFO 構造体
列挙可能かどうかなど、ガベージ コレクション ヒープに関する情報が提供されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _COR_HEAPINFO {  
    BOOL areGCStructuresValid;
    DWORD pointerSize;
    DWORD numHeaps;  
    BOOL concurrent;
    CorDebugGCType gcType;
} COR_HEAPINFO;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`areGCStructuresValid`|`true`ガベージ コレクション構造体が有効で、ヒープを列挙できる場合。それ以外`false`の場合は、 .|  
|`pointerSize`|ターゲット アーキテクチャ上のポインターのサイズ (バイト単位)。|  
|`numHeaps`|プロセス内の論理ガーベッジ・コレクション・ヒープの数。|  
|`concurrent`|`TRUE`同時実行 (バックグラウンド) ガベージ コレクションが有効になっている場合。それ以外`FALSE`の場合は、 .|  
|`gcType`|ガベージ コレクターがワークステーションまたはサーバーで実行されているかどうかを示す[CorDebugGCType](cordebuggctype-enumeration.md)列挙体のメンバー。|  
  
## <a name="remarks"></a>解説  
 構造体の`COR_HEAPINFO`インスタンスは[、メソッドを](icordebugprocess5-getgcheapinformation-method.md)呼び出すことによって返されます。  
  
 ガベージ コレクション ヒープ上のオブジェクトを列挙する前に、必ず`areGCStructuresValid`フィールドをチェックして、ヒープが列挙可能な状態にあることを確認する必要があります。 詳細については、メソッドを参照[してください](icordebugprocess5-getgcheapinformation-method.md)。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
