---
title: CorCheckDuplicatesFor 列挙型
ms.date: 03/30/2017
api_name:
- CorCheckDuplicatesFor
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorCheckDuplicatesFor
helpviewer_keywords:
- CorCheckDuplicatesFor enumeration [.NET Framework metadata]
ms.assetid: d8ec8d3c-70f7-4cc6-9957-68068fd8f49c
topic_type:
- apiref
ms.openlocfilehash: 2985c419b25b8bf76df8fee0f0f37ba9ebee3df7
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007903"
---
# <a name="corcheckduplicatesfor-enumeration"></a>CorCheckDuplicatesFor 列挙型
重複をチェックするメタデータトークンを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorCheckDuplicatesFor {  
  
    MDDupAll                    = 0xffffffff,  
    MDDupENC                    = MDDupAll,  
    MDNoDupChecks               = 0x00000000,  
    MDDupTypeDef                = 0x00000001,  
    MDDupInterfaceImpl          = 0x00000002,  
    MDDupMethodDef              = 0x00000004,  
    MDDupTypeRef                = 0x00000008,  
    MDDupMemberRef              = 0x00000010,  
    MDDupCustomAttribute        = 0x00000020,  
    MDDupParamDef               = 0x00000040,  
    MDDupPermission             = 0x00000080,  
    MDDupProperty               = 0x00000100,  
    MDDupEvent                  = 0x00000200,  
    MDDupFieldDef               = 0x00000400,  
    MDDupSignature              = 0x00000800,  
    MDDupModuleRef              = 0x00001000,  
    MDDupTypeSpec               = 0x00002000,  
    MDDupImplMap                = 0x00004000,  
    MDDupAssemblyRef            = 0x00008000,  
    MDDupFile                   = 0x00010000,  
    MDDupExportedType           = 0x00020000,  
    MDDupManifestResource       = 0x00040000,  
    MDDupGenericParam           = 0x00080000,  
    MDDupMethodSpec             = 0x00100000,  
    MDDupGenericParamConstraint = 0x00200000,  
  
    MDDupAssembly               = 0x10000000,  
  
    MDDupDefault =
        MDNoDupChecks | MDDupTypeRef | MDDupMemberRef |
        MDDupSignature | MDDupTypeSpec | MDDupMethodSpec  
  
} CorCheckDuplicatesFor;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`MDDupAll`|すべてのメタデータトークンの重複を確認します。|  
|`MDDupENC`|使用されていません。|  
|`MDNoDupChecks`|メタデータトークンの重複をチェックしないでください。|  
|`MDDupTypeDef`|トークンの重複を確認 `mdTypeDef` します。|  
|`MDDupInterfaceImpl`|トークンの重複を確認 `mdInterfaceImpl` します。|  
|`MDDupMethodDef`|トークンの重複を確認 `mdMethodDef` します。|  
|`MDDupTypeRef`|トークンの重複を確認 `mdTypeRef` します。|  
|`MDDupMemberRef`|トークンの重複を確認 `mdMemberRef` します。|  
|`MDDupCustomAttribute`|トークンの重複を確認 `mdCustomAttribute` します。|  
|`MDDupParamDef`|トークンの重複を確認 `mdParamDef` します。|  
|`MDDupPermission`|トークンの重複を確認 `mdPermission` します。|  
|`MDDupProperty`|トークンの重複を確認 `mdProperty` します。|  
|`MDDupEvent`|トークンの重複を確認 `mdEvent` します。|  
|`MDDupFieldDef`|トークンの重複を確認 `mdFieldDef` します。|  
|`MDDupSignature`|トークンの重複を確認 `mdSignature` します。|  
|`MDDupModuleRef`|トークンの重複を確認 `mdModuleRef` します。|  
|`MDDupTypeSpec`|トークンの重複を確認 `mdTypeSpec` します。|  
|`MDDupImplMap`|トークンの重複を確認 `mdImplMap` します。|  
|`MDDupAssemblyRef`|トークンの重複を確認 `mdAssemblyRef` します。|  
|`MDDupFile`|トークンの重複を確認 `mdFile` します。|  
|`MDDupExportedType`|トークンの重複を確認 `mdExportedType` します。|  
|`MDDupManifestResource`|トークンの重複を確認 `mdManifestResource` します。|  
|`MDDupGenericParam`|トークンの重複を確認 `mdGenericParam` します。|  
|`MDDupMethodSpec`|トークンの重複を確認 `mdMethodSpec` します。|  
|`MDDupGenericParamConstraint`|トークンの重複を確認 `mdGenericParamConstraint` します。|  
|`MDDupAssembly`|トークンの重複を確認 `mdAssembly` します。|  
|`MDDupDefault`|、、、、およびの各トークンの重複を確認 `mdMemberRef` `mdTypeRef` `mdSignature` `mdTypeSpec` `mdMethodSpec` します。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorHdr. h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ列挙体](metadata-enumerations.md)
