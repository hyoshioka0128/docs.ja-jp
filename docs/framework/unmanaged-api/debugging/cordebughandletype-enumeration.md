---
title: CorDebugHandleType 列挙型
ms.date: 03/30/2017
api_name:
- CorDebugHandleType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugHandleType
helpviewer_keywords:
- CorDebugHandleType enumeration [.NET Framework debugging]
ms.assetid: 84296b55-c2c5-424c-ac9c-8e28e2895945
topic_type:
- apiref
ms.openlocfilehash: 2d296c1778e00c4c72e860e0705994518d1481e8
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795884"
---
# <a name="cordebughandletype-enumeration"></a>CorDebugHandleType 列挙型
ハンドル型を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorDebugHandleType {  
    HANDLE_STRONG                  = 1,  
    HANDLE_WEAK_TRACK_RESURRECTION = 2  
} CorDebugHandleType;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`HANDLE_STRONG`|ハンドルは strong であり、ガベージコレクションによってオブジェクトが解放されるのを防ぎます。|  
|`HANDLE_WEAK_TRACK_RESURRECTION`|ハンドルは脆弱であり、ガベージコレクションによってオブジェクトが解放されるのを防ぐことはできません。<br /><br /> オブジェクトが収集されると、ハンドルは無効になります。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のデバッグ](debugging-enumerations.md)
