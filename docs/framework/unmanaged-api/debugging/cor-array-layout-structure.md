---
title: COR_ARRAY_LAYOUT 構造体
ms.date: 03/30/2017
api_name:
- COR_ARRAY_LAYOUT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_ARRAY_LAYOUT
helpviewer_keywords:
- COR_DEBUG_IL_TO_NATIVE_MAP structure [.NET Framework debugging]
ms.assetid: aa20ac3d-6f60-4aa2-91c5-f3a86f82eba8
topic_type:
- apiref
ms.openlocfilehash: ca2d00611a7530dfb0d1c2a27123947bdf69820d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179350"
---
# <a name="cor_array_layout-structure"></a>COR_ARRAY_LAYOUT 構造体
メモリ内の配列オブジェクトのレイアウトに関する情報が提供されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct COR_ARRAY_LAYOUT {  
    COR_TYPEID componentID;  
    CorElementType componentType;  
    ULONG32 firstElementOffset;  
    ULONG32 elementSize;  
    ULONG32 countOffset;
    ULONG32 rankSize;
    ULONG32 numRanks;
    ULONG32 rankOffset;
} COR_ARRAY_LAYOUT;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`componentID`|配列に含まれるオブジェクトの型の識別子。|  
|`componentType`|コンポーネントがガベージ コレクション参照、値クラス、またはプリミティブであるかどうかを示す CorElementType 列挙値。|  
|`firstElementOffset`|配列の最初の要素へのオフセット。|  
|`elementSize`|各要素のサイズ。|  
|`countOffset`|配列内の要素数のオフセット。|  
|`rankSize`|ランクのサイズ (バイト単位)。|  
|`numRanks`|配列内のランクの数。|  
|`rankOffset`|ランクの開始位置のオフセット。|  
  
## <a name="remarks"></a>解説  
 この`rankSize`フィールドは、多次元配列のランクのサイズを指定します。 これは、単一次元配列でも正確です。  
  
 1 次元`numRanks`配列の場合は 1、次元`N`の多次元配列の`N`場合は、値は 1 です。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
