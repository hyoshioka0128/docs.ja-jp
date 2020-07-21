---
title: COR_PRF_JIT_CACHE 列挙型
ms.date: 03/30/2017
api_name:
- COR_PRF_JIT_CACHE
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_JIT_CACHE
helpviewer_keywords:
- COR_PRF_JIT_CACHE enumeration [.NET Framework profiling]
ms.assetid: e7b8f6b4-95bc-4ba5-b9eb-f5590a7326a4
topic_type:
- apiref
ms.openlocfilehash: d19d7ed2262db6d3c6e7f15db0e96da52f86db4a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500859"
---
# <a name="cor_prf_jit_cache-enumeration"></a>COR_PRF_JIT_CACHE 列挙型
キャッシュされている関数検索の結果を示します。  
  
> [!NOTE]
> `COR_PRF_CACHED_FUNCTION_FOUND`の値は0であるため、 `COR_PRF_JIT_CACHE` ブールサロゲートとして使用することはできません。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    COR_PRF_CACHED_FUNCTION_FOUND,  
    COR_PRF_CACHED_FUNCTION_NOT_FOUND  
} COR_PRF_JIT_CACHE;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`COR_PRF_FUNCTION_FOUND`|検索によって関数が検出されました。|  
|`COR_PRF_FUNCTION_NOT_FOUND`|検索で関数が見つかりませんでした。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のプロファイリング](profiling-enumerations.md)
