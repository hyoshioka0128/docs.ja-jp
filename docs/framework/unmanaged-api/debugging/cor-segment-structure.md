---
title: COR_SEGMENT 構造体
ms.date: 03/30/2017
api_name:
- COR_SEGMENT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_SEGMENT
helpviewer_keywords:
- COR_SEGMENT structure [.NET Framework debugging]
ms.assetid: 93aeecb9-7fef-4545-8daf-f566dfc47084
topic_type:
- apiref
ms.openlocfilehash: a5c743064b8ca645cf45d02b8800c88187bf4c6c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179280"
---
# <a name="cor_segment-structure"></a>COR_SEGMENT 構造体
マネージド ヒープのメモリ領域に関する情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _COR_SEGMENT {  
    CORDB_ADDRESS start;
    CORDB_ADDRESS end;
    CorDebugGenerationTypes gen;
    ULONG heap;
} COR_SEGMENT;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`start`|メモリ領域の開始アドレス。|  
|`end`|メモリ領域の終了アドレス。|  
|`gen`|メモリ領域の生成を示す [CorDebugGenerationTypes](cordebuggenerationtypes-enumeration.md) 列挙メンバー。|  
|`heap`|メモリ領域が存在するヒープ番号。 詳細については、「解説」を参照してください。|  
  
## <a name="remarks"></a>解説  
 `COR_SEGMENTS` 構造体は、マネージド ヒープのメモリ領域を表します。  `COR_SEGMENTS` オブジェクトは、[ICorDebugProcess5::EnumerateHeapRegions](icordebugprocess5-enumerateheapregions-method.md) メソッドを呼び出すことによって入力される [ICorDebugHeapRegionEnum](icordebugheapsegmentenum-interface.md) コレクション オブジェクトのメンバーです。  
  
 `heap` フィールドは、報告されたヒープに対応するプロセッサ番号です。 ワークステーション ガベージ コレクターでは、ワークステーションにガベージ コレクション ヒープが 1 つしかないため、その値は常に 0 です。 サーバー ガベージ コレクターでは、その値はヒープがアタッチされているプロセッサに対応します。 ガベージ コレクターの実装の詳細が原因で、実際のプロセッサ数よりも、ガベージ コレクション ヒープが多かったり少なかったりする場合があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ構造体](debugging-structures.md)
- [デバッグ](index.md)
