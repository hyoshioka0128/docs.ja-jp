---
title: CorDebugIlToNativeMappingTypes 列挙型
ms.date: 03/30/2017
api_name:
- CorDebugIlToNativeMappingTypes
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugIlToNativeMappingTypes
helpviewer_keywords:
- CorDebugIIToNativeMappingTypes enumeration [.NET Framework debugging]
ms.assetid: c35e2919-42c3-4ba0-ae28-443c35f66f93
topic_type:
- apiref
ms.openlocfilehash: 808fc70a308eff1b05aa49ea2bb89fe53377c973
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795847"
---
# <a name="cordebugiltonativemappingtypes-enumeration"></a>CorDebugIlToNativeMappingTypes 列挙型
COR_DEBUG_IL_TO_NATIVE_MAP 構造体のインスタンスによって表されるネイティブ命令の特定の範囲が、特別なコード領域に対応するかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorDebugIlToNativeMappingTypes {  
    NO_MAPPING = -1,  
    PROLOG     = -2,  
    EPILOG     = -3  
} CorDebugIlToNativeMappingTypes;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`NO_MAPPING`|ネイティブ命令の範囲は、特別なコード領域には対応していません。|  
|`PROLOG`|ネイティブ命令の範囲は、プロローグに対応しています。|  
|`EPILOG`|ネイティブ命令の範囲は、エピローグに相当します。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetILToNativeMapping メソッド](icordebugcode-getiltonativemapping-method.md)
- [列挙体のデバッグ](debugging-enumerations.md)
