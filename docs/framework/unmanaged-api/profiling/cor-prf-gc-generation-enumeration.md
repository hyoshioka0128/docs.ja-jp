---
title: COR_PRF_GC_GENERATION 列挙型
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_GENERATION
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_GENERATION
helpviewer_keywords:
- COR_GC_GENERATION_FLAGS enumeration [.NET Framework profiling]
ms.assetid: d6ece160-26ad-4d39-abd7-05acd6f78c48
topic_type:
- apiref
ms.openlocfilehash: b7a068efcf20b2028e9c193567d15b59e582febf
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500924"
---
# <a name="cor_prf_gc_generation-enumeration"></a>COR_PRF_GC_GENERATION 列挙型
ガベージコレクションの生成を識別します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    COR_PRF_GC_GEN_0 = 0,  
    COR_PRF_GC_GEN_1 = 1,  
    COR_PRF_GC_GEN_2 = 2,  
    COR_PRF_GC_LARGE_OBJECT_HEAP = 3,
    COR_PRF_GC_PINNED_OBJECT_HEAP= 4
} COR_PRF_GC_GENERATION;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`COR_PRF_GC_GEN_0`|オブジェクトは、ジェネレーション0として格納されます。|  
|`COR_PRF_GC_GEN_1`|オブジェクトは、ジェネレーション1として格納されます。|  
|`COR_PRF_GC_GEN_2`|オブジェクトは、ジェネレーション2として格納されます。|  
|`COR_PRF_GC_LARGE_OBJECT_HEAP`|オブジェクトは、ラージオブジェクトヒープに格納されます。|  
|`COR_PRF_GC_PINNED_OBJECT_HEAP`|オブジェクトは、固定されたオブジェクトヒープに格納されます。|  
  
## <a name="remarks"></a>解説  
 ガベージコレクターは、オブジェクトを経過期間に基づいてジェネレーションに分割することによって、メモリ管理のパフォーマンスを向上させます。 現在、ガベージコレクターは、番号0、1、および2の3つのジェネレーションと、2つの特殊なヒープセグメント (大きなオブジェクト用とピン留めオブジェクト用) を使用しています。
  
 サイズがしきい値を超えるオブジェクトは、大きなオブジェクトヒープに格納されます。 ピン留めされたオブジェクトは、通常のヒープに割り当てた場合のパフォーマンスコストを回避するために、固定されたオブジェクトヒープに割り当てることができます。 割り当てられた他のオブジェクトは、ジェネレーション0に属しています。 ジェネレーション0でガベージコレクションが発生した後に存在するすべてのオブジェクトは、ジェネレーション1に昇格されます。 ジェネレーション1でガベージコレクションが発生した後に存在するオブジェクトは、ジェネレーション2に移動します。  
  
 ジェネレーションを使用することは、ガベージコレクターが、割り当てられたオブジェクトのサブセットだけを一度に処理する必要があることを意味します。  
  
 `COR_PRF_GC_GENERATION`列挙体は、 [COR_PRF_GC_GENERATION_RANGE](cor-prf-gc-generation-range-structure.md)構造体によって使用されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のプロファイリング](profiling-enumerations.md)
