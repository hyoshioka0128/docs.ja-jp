---
title: CorNotificationForTokenMovement 列挙型
ms.date: 03/30/2017
api_name:
- CorNotificationForTokenMovement
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorNotificationForTokenMovement
helpviewer_keywords:
- CorNotificationForTokenMovement enumeration [.NET Framework metadata]
ms.assetid: 1edd1670-976a-4fc8-bef7-7c41e60ad989
topic_type:
- apiref
ms.openlocfilehash: e8065a5492884a4b7f5d662737e4beddc6fca5b3
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007599"
---
# <a name="cornotificationfortokenmovement-enumeration"></a>CorNotificationForTokenMovement 列挙型
トークンの再マップが発生したときにメタデータ API クライアントに送信される通知を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorNotificationForTokenMovement {  
  
    MDNotifyDefault             = 0x0000000f,  
    MDNotifyAll                 = 0xffffffff,  
    MDNotifyNone                = 0x00000000,  
    MDNotifyMethodDef           = 0x00000001,  
    MDNotifyMemberRef           = 0x00000002,  
    MDNotifyFieldDef            = 0x00000004,  
    MDNotifyTypeRef             = 0x00000008,  
  
    MDNotifyTypeDef             = 0x00000010,  
    MDNotifyParamDef            = 0x00000020,  
    MDNotifyInterfaceImpl       = 0x00000040,  
    MDNotifyProperty            = 0x00000080,  
    MDNotifyEvent               = 0x00000100,  
    MDNotifySignature           = 0x00000200,  
    MDNotifyTypeSpec            = 0x00000400,  
    MDNotifyCustomAttribute     = 0x00000800,  
    MDNotifySecurityValue       = 0x00001000,  
    MDNotifyPermission          = 0x00002000,  
    MDNotifyModuleRef           = 0x00004000,  
  
    MDNotifyNameSpace           = 0x00008000,  
  
    MDNotifyAssemblyRef         = 0x01000000,  
    MDNotifyFile                = 0x02000000,  
    MDNotifyExportedType        = 0x04000000,  
    MDNotifyResource            = 0x08000000  
  
} CorNotificationForTokenMovement;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`MDNotifyDefault`|、、 `mdTypeRef` `mdMethodDef` `mdMemberRef` 、またはトークンが移動したときに通知 `mdFieldDef` します。|  
|`MDNotifyAll`|任意のトークンが移動したときに通知します。|  
|`MDNotifyNone`|トークンの移動時に通知しません。|  
|`MDNotifyMethodDef`|トークンが移動したときに通知 `mdMethodDef` します。|  
|`MDNotifyMemberRef`|トークンが移動したときに通知 `mdMemberRef` します。|  
|`MDNotifyFieldDef`|トークンが移動したときに通知 `mdFieldDef` します。|  
|`MDNotifyTypeRef`|トークンが移動したときに通知 `mdTypeRef` します。|  
|`MDNotifyTypeDef`|トークンが移動したときに通知 `mdTypeDef` します。|  
|`MDNotifyParamDef`|トークンが移動したときに通知 `mdParamDef` します。|  
|`MDNotifyInterfaceImpl`|トークンが移動したときに通知 `mdInterfaceImpl` します。|  
|`MDNotifyProperty`|トークンが移動したときに通知 `mdProperty` します。|  
|`MDNotifyEvent`|トークンが移動したときに通知 `mdEvent` します。|  
|`MDNotifySignature`|トークンが移動したときに通知 `mdSignature` します。|  
|`MDNotifyTypeSpec`|トークンが移動したときに通知 `mdTypeSpec` します。|  
|`MDNotifyCustomAttribute`|トークンが移動したときに通知 `mdCustomAttribute` します。|  
|`MDNotifySecurityValue`|トークンが移動したときに通知 `mdSecurityValue` します。|  
|`MDNotifyPermission`|トークンが移動したときに通知 `mdPermission` します。|  
|`MDNotifyModuleRef`|トークンが移動したときに通知 `mdModuleRef` します。|  
|`MDNotifyNameSpace`|トークンが移動したときに通知 `mdNameSpace` します。|  
|`MDNotifyAssemblyRef`|トークンが移動したときに通知 `mdAssemblyRef` します。|  
|`MDNotifyFile`|トークンが移動したときに通知 `mdFile` します。|  
|`MDNotifyExportedType`|トークンが移動したときに通知 `mdExportedType` します。|  
|`MDNotifyResource`|トークンが移動したときに通知 `mdManifestResource` します。|  
  
## <a name="remarks"></a>コメント  
 メタデータのマージ中に、トークンが再マップ (移動) される場合があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorHdr. h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ列挙体](metadata-enumerations.md)
