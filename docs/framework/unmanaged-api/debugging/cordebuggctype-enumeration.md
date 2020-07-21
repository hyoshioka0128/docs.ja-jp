---
title: CorDebugGCType 列挙型
ms.date: 03/30/2017
api_name:
- CorDebugGCType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugGCType
helpviewer_keywords:
- CorDebugGCType enumeration [.NET Framework debugging]
ms.assetid: 880ca92a-42d4-42a5-9b9c-c2848eb39c6a
topic_type:
- apiref
ms.openlocfilehash: 8dd070d2c895a94ac996be81e672bd67f59b83b7
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795899"
---
# <a name="cordebuggctype-enumeration"></a>CorDebugGCType 列挙型
ガベージ コレクターがワークステーションまたはサーバーのどちらで実行されているかを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorDebugGCType {  
    CorDebugWorkstationGC  = 0,  
    CorDebugServerGC       = ( CorDebugWorkstationGC + 1 )  
} CorDebugGCType;  
```  
  
## <a name="parameters"></a>パラメーター  
  
## <a name="members"></a>メンバー  
  
|メンバー名|説明|  
|-----------------|-----------------|  
|`CorDebugWorkstationGC`|ガベージコレクターはワークステーション上で実行されています。|  
|`CorDebugServerGC`|ガベージコレクターはサーバーで実行されています。|  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のデバッグ](debugging-enumerations.md)
