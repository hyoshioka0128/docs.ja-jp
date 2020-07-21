---
title: LogSwitchCallReason 列挙型
ms.date: 03/30/2017
api_name:
- LogSwitchCallReason
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- LogSwitchCallReason
helpviewer_keywords:
- LogSwitchCallReason enumeration [.NET Framework debugging]
ms.assetid: 5bbb8d1b-bbc4-47b0-b1b1-2d54cc0be291
topic_type:
- apiref
ms.openlocfilehash: 4d29bb3886ffb51e1dfb9654f4d70ef7c568fd43
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420709"
---
# <a name="logswitchcallreason-enumeration"></a>LogSwitchCallReason 列挙型
デバッグとトレースの切り替えで実行された操作を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum LogSwitchCallReason {  
    SWITCH_CREATE,  
    SWITCH_MODIFY,  
    SWITCH_DELETE  
} LogSwitchCallReason;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`SWITCH_CREATE`|デバッグ/トレーススイッチが作成されました。|  
|`SWITCH_MODIFY`|デバッグ/トレーススイッチが変更されました。|  
|`SWITCH_DELETE`|デバッグ/トレーススイッチが削除されました。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のデバッグ](debugging-enumerations.md)
