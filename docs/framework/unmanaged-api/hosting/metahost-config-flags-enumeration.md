---
title: METAHOST_CONFIG_FLAGS 列挙体
ms.date: 03/30/2017
api_name:
- METAHOST_CONFIG_FLAGS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- METAHOST_CONFIG_FLAGS
helpviewer_keywords:
- METAHOST_CONFIG_FLAGS enumeration [.NET Framework hosting]
ms.assetid: 6f1e389f-ed99-4d6a-a0ba-72d7d869a01d
topic_type:
- apiref
ms.openlocfilehash: 6b37fcfc04e3ec880c67f102ec12d7f3e4b06a43
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84493163"
---
# <a name="metahost_config_flags-enumeration"></a>METAHOST_CONFIG_FLAGS 列挙体
`pdwConfigFlags` [ICLRMetaHostPolicy:: GetRequestedRuntime](iclrmetahostpolicy-getrequestedruntime-method.md)メソッドのパラメーターで返されるフラグについて説明します。これは、 `useLegacyV2RuntimeActivationPolicy` 構成ファイルの[ \<startup> 要素](../../configure-apps/file-schema/startup/startup-element.md)内の属性の存在と設定を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_UNSET  = 0x00,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_TRUE   = 0x01,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_FALSE  = 0x02,  
    METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_MASK   = 0x03  
} METAHOST_CONFIG_FLAGS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_UNSET`|`useLegacyV2RuntimeActivationPolicy`属性が[ \<startup> 要素](../../configure-apps/file-schema/startup/startup-element.md)内に存在しませんでした。|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_TRUE`|`useLegacyV2RuntimeActivationPolicy`属性が存在し、がに設定されて `true` います。|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_FALSE`|`useLegacyV2RuntimeActivationPolicy`属性が存在し、がに設定されて `false` います。|  
|`METAHOST_CONFIG_FLAGS_LEGACY_V2_ACTIVATION_POLICY_MASK`|に関連する値を取得するには、このマスクをで返される値に適用 `pdwConfigFlags` `useLegacyV2RuntimeActivationPolicy` します。|  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** メタホスト .h  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスティングの列挙型](hosting-enumerations.md)
- [GetRequestedRuntime メソッド](iclrmetahostpolicy-getrequestedruntime-method.md)
- [\<startup> 要素](../../configure-apps/file-schema/startup/startup-element.md)
