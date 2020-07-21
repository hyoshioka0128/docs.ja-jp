---
title: COR_GC_THREAD_STATS 構造体
ms.date: 03/30/2017
api_name:
- COR_GC_THREAD_STATS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_THREAD_STATS
helpviewer_keywords:
- COR_GC_THREAD_STATS structure [.NET Framework hosting]
ms.assetid: 01f9a59b-7679-4d42-9ced-4a8981625c3d
topic_type:
- apiref
ms.openlocfilehash: 88e81779fc9c20c506f3b0aa11ac2da3958dfe86
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616698"
---
# <a name="cor_gc_thread_stats-structure"></a>COR_GC_THREAD_STATS 構造体
ガベージコレクションに関連するスレッドごとの統計情報を格納します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _COR_GC_THREAD_STATS {  
    ULONGLONG  PerThreadAllocation;
    ULONG      Flags;
} COR_GC_THREAD_STATS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`PerThreadAllocation`|現在のインスタンスに関連付けられているスレッドに割り当てられたメモリのバイト数 `COR_GC_THREAD_STATS` 。 ジェネレーション0のガベージコレクションが発生するたびに、この数値はゼロにクリアされます。|  
|`Flags`|最新のガベージコレクションで上位のジェネレーションに昇格されたバイト数。|  
  
## <a name="remarks"></a>解説  
 [ICLRTask:: GetMemStats](iclrtask-getmemstats-method.md)は、型の出力パラメーターを受け取り `COR_GC_THREAD_STATS` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** GCHost  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト構造体](hosting-structures.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
