---
title: IMethodMalloc インターフェイス
ms.date: 03/30/2017
api_name:
- IMethodMalloc
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- IMethodMalloc
helpviewer_keywords:
- IMethodMalloc interface [.NET Framework profiling]
ms.assetid: 8c8ab5dc-557c-473a-82f2-6e403eca7dac
topic_type:
- apiref
ms.openlocfilehash: 12b97b28383eb7c39f20ee0e88f55d48e60ad956
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494112"
---
# <a name="imethodmalloc-interface"></a>IMethodMalloc インターフェイス
新しい Microsoft 中間言語 (MSIL) 関数の本体にメモリを割り当てる方法を提供します。  
  
> [!NOTE]
> インターフェイスは、 `IMethodMalloc` 単純なメモリアロケーターです。 メモリを割り当てることはできますが、解放することはできません。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Alloc メソッド](imethodmalloc-alloc-method.md)|新しい MSIL 関数本体に指定された量のメモリを割り当てようとします。|  
  
## <a name="remarks"></a>解説  
 各アロケーターはモジュール固有であり、関数本体がモジュールのベースから正のオフセットになるようにします。 モジュールのベースを超えるメモリは貴重な場合があるため、アロケーターを使用して、関数本体にのみメモリを割り当てる必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
