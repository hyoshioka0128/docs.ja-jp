---
title: CREATE_ASM_NAME_OBJ_FLAGS 列挙型
ms.date: 03/30/2017
api_name:
- CREATE_ASM_NAME_OBJ_FLAGS
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- CREATE_ASM_NAME_OBJ_FLAGS
helpviewer_keywords:
- CREATE_ASM_NAME_OBJ_FLAGS enumeration [.NET Framework fusion]
ms.assetid: a5ed2fd0-c7d2-4603-aaca-5d0caad92675
topic_type:
- apiref
ms.openlocfilehash: ee856dbd398d0fa5e3eee7d9b2b2cfc7c7a57ecf
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176592"
---
# <a name="create_asm_name_obj_flags-enumeration"></a>CREATE_ASM_NAME_OBJ_FLAGS 列挙型
関数によって構築されるときに[、IAssemblyName インターフェイス](iassemblyname-interface.md)オブジェクトの属性を指定[します](createassemblynameobject-function.md)。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
  
    CANOF_PARSE_DISPLAY_NAME            = 0x1,  
    CANOF_SET_DEFAULT_VALUES            = 0x2,  
    CANOF_VERIFY_FRIEND_ASSEMBLYNAME    = 0x4,  
    CANOF_PARSE_FRIEND_DISPLAY_NAME     =
        CANOF_PARSE_DISPLAY_NAME | CANOF_VERIFY_FRIEND_ASSEMBLYNAME  
  
} CREATE_ASM_NAME_OBJ_FLAGS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`CANOF_PARSE_DISPLAY_NAME`|渡されたパラメーターがテキスト ID であることを示します。|  
|`CANOF_SET_DEFAULT_VALUES`|いくつかのデフォルト値を設定します。|  
|`CANOF_VERIFY_FRIEND_ASSEMBLYNAME`|フレンド アセンブリの規則を検証します (名前と公開キーのみ)。 このメンバーは内部使用専用です。|  
|`CANOF_PARSE_FRIEND_DISPLAY_NAME`|`CANOF_PARSE_DISPLAY_NAME`フラグと フラグ`CANOF_VERIFY_FRIEND_ASSEMBLYNAME`の組み合わせ。 このメンバーは内部使用専用です。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** フュージョン.h  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IAssemblyName インターフェイス](iassemblyname-interface.md)
- [CreateAssemblyNameObject 関数](createassemblynameobject-function.md)
- [fusion 列挙体](fusion-enumerations.md)
