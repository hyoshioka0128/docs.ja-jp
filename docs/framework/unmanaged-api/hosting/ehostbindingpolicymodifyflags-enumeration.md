---
title: EHostBindingPolicyModifyFlags 列挙型
ms.date: 03/30/2017
api_name:
- EHostBindingPolicyModifyFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EHostBindingPolicyModifyFlags
helpviewer_keywords:
- EHostBindingPolicyModifyFlags enumeration [.NET Framework hosting]
ms.assetid: 0339af16-ee1d-48ec-837d-a79d9a9c89f8
topic_type:
- apiref
ms.openlocfilehash: 256c362ae0aea51fea16ce799db243b105dee81a
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616243"
---
# <a name="ehostbindingpolicymodifyflags-enumeration"></a>EHostBindingPolicyModifyFlags 列挙型
ソースアセンブリからターゲットアセンブリにポリシー変更を適用するときに、共通言語ランタイム (CLR) が実行するリダイレクトの種類をホストが指定できるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum _hostBindingPolicyModifyFlags {  
    HOST_BINDING_POLICY_MODIFY_DEFAULT  = 0,  
    HOST_BINDING_POLICY_MODIFY_CHAIN    = 1,  
    HOST_BINDING_POLICY_MODIFY_REMOVE   = 2,  
    HOST_BINDING_POLICY_MODIFY_MAX      = 3  
} EHostBindingPolicyModifyFlags;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`HOST_BINDING_POLICY_MODIFY_CHAIN`|CLR がソースアセンブリのポリシー値をターゲットアセンブリのポリシー値に連結するように指定します。|  
|`HOST_BINDING_POLICY_MODIFY_DEFAULT`|CLR が既定のアクションを実行することを指定します。|  
|`HOST_BINDING_POLICY_MODIFY_MAX`|CLR がターゲットアセンブリのポリシー値を最大値に設定することを指定します。|  
|`HOST_BINDING_POLICY_MODIFY_REMOVE`|CLR がターゲットアセンブリのポリシー値をソースアセンブリのポリシー値に置き換えることを指定します。|  
  
## <a name="remarks"></a>解説  
 [ICLRHostBindingPolicyManager:: ModifyApplicationPolicy](iclrhostbindingpolicymanager-modifyapplicationpolicy-method.md)メソッドは、型のパラメーターを受け取り `EHostBindingPolicyModifyFlags` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRHostBindingPolicyManager インターフェイス](iclrhostbindingpolicymanager-interface.md)
- [ホスティングの列挙体](hosting-enumerations.md)
