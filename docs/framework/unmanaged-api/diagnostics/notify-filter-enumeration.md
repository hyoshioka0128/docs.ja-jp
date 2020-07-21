---
title: NOTIFY_FILTER 列挙体
ms.date: 03/30/2017
api_name:
- NOTIFY_FILTER
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- NOTIFY_FILTER
helpviewer_keywords:
- NOTIFY_FILTER enumeration [.NET Framework debugging]
ms.assetid: 4789d08f-8683-45d3-ac30-73d48c61e470
topic_type:
- apiref
ms.openlocfilehash: b20e18d5f4314a0ab1442ac7bd5c6514e4db85d5
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609483"
---
# <a name="notify_filter-enumeration"></a>NOTIFY_FILTER 列挙体
デバッガー関数のコールバックを識別します。 詳細については、 [INotifySource2:: SetNotifyFilter](inotifysource2-setnotifyfilter-method.md)メソッドを参照してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
enum tagNOTIFY_FILTER  
{  
    NOTIFY_FILTER_ONSYNCCALLOUT    = 0x1,  
    NOTIFY_FILTER_ONSYNCCALLENTER  = 0x2,  
    NOTIFY_FILTER_ONSYNCCALLEXIT   = 0x4,  
    NOTIFY_FILTER_ONSYNCCALLRETURN = 0x8,  
    NOTIFY_FILTER_ALLSYNC = NOTIFY_FILTER_ONSYNCCALLOUT | NOTIFY_FILTER_ONSYNCCALLENTER | NOTIFY_FILTER_ONSYNCCALLEXIT | NOTIFY_FILTER_ONSYNCCALLRETURN,  
    NOTIFY_FILTER_ALL              = 0xffffffff,  
    NOTIFY_FILTER_NONE             = 0  
};  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`NOTIFY_FILTER_ONSYNCCALLOUT`|[INotifySink2:: OnSyncCallOut](inotifysink2-onsynccallout-method.md)メソッドを呼び出す必要があることを示します。|  
|`NOTIFY_FILTER_ONSYNCCALLENTER`|[INotifySink2:: OnSyncCallEnter](inotifysink2-onsynccallenter-method.md)メソッドを呼び出す必要があることを示します。|  
|`NOTIFY_FILTER_ONSYNCCALLEXIT`|[INotifySink2:: OnSyncCallExit](inotifysink2-onsynccallexit-method.md)メソッドを呼び出す必要があることを示します。|  
|`NOTIFY_FILTER_ONSYNCCALLRETURN`|[INotifySink2:: OnSyncCallReturn](inotifysink2-onsynccallreturn-method.md)メソッドを呼び出す必要があることを示します。|  
|`NOTIFY_FILTER_ALLSYNC`|すべての[INotifySink2](inotifysink2-interface.md)メソッドを呼び出す必要があることを示します。|  
|`NOTIFY_FILTER_ALL`|既存の通知と今後の通知をすべてアクティブにします。|  
|`NOTIFY_FILTER_NONE`|通知メソッドを呼び出さないことを示します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** ProtocolNotify2  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断列挙型](diagnostics-symbol-store-enumerations.md)
