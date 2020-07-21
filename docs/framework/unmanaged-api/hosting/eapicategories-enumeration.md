---
title: EApiCategories 列挙型
ms.date: 03/30/2017
api_name:
- EApiCategories
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EApiCategories
helpviewer_keywords:
- EApiCategories enumeration [.NET Framework hosting]
ms.assetid: 3c4a8a5a-8a46-4ac9-947f-4959bc9d6ac6
topic_type:
- apiref
ms.openlocfilehash: d31b0190ef9a697fb27c849db080bec6c57618ae
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616386"
---
# <a name="eapicategories-enumeration"></a>EApiCategories 列挙型
部分的に信頼されたコードでホストが実行をブロックできる機能のカテゴリについて説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    eNoCategory               = 0,  
    eSynchronization          = 0x1,  
    eSharedState              = 0x2,  
    eExternalProcessMgmt      = 0x4,  
    eSelfAffectingProcessMgmt = 0x8,  
    eExternalThreading        = 0x10,  
    eSelfAffectingThreading   = 0x20,  
    eSecurityInfrastructure   = 0x40,  
    eUI                       = 0x80,  
    eMayLeakOnAbort           = 0x100,  
    eAll                      = 0x1ff  
} EHostProtectionCategories;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`eAll`|他のフィールドの対象となるすべてのマネージクラスおよびメンバーが、 `EApiCategories` 部分的に信頼されたコードでの実行をブロックされるように指定します。|  
|`eExternalProcessMgmt`|外部プロセスの作成、操作、および破棄を許可するマネージクラスおよびメンバーが、部分的に信頼されたコードでの実行をブロックされることを指定します。|  
|`eExternalThreading`|外部スレッドの作成、操作、および破棄を許可するマネージクラスおよびメンバーが、部分的に信頼されたコードでの実行をブロックされることを指定します。|  
|`eMayLeakOnAbort`|中止時にメモリをリークする可能性のあるマネージ型およびメンバーが、部分的に信頼されたコードで実行されないようにブロックすることを指定します。|  
|`eNoCategory`|部分的に信頼されたコードでは、マネージコードのカテゴリの実行をブロックしないことを指定します。|  
|`eSecurityInfrastructure`|共通言語ランタイム (CLR) のセキュリティインフラストラクチャが、部分的に信頼されたコードによって使用されるのをブロックすることを指定します。|  
|`eSelfAffectingProcessMgmt`|ホストされるプロセスに影響を与える可能性があるマネージクラスおよびメンバーが、部分的に信頼されたコードで実行されないように指定します。|  
|`eSelfAffectingThreading`|ホストされているプロセスのスレッドに影響を与える可能性のあるマネージクラスおよびメンバーが、部分的に信頼されたコードでの実行をブロックされるように指定します。|  
|`eSharedState`|マネージクラスおよび共有状態を公開するメンバーが、部分的に信頼されたコードで実行されないようにブロックすることを指定します。|  
|`eSynchronization`|ユーザーコードがロックを保持することを許可する共通言語ランタイムクラスおよびメンバーが、部分的に信頼されたコードでの実行をブロックするように指定します。|  
|`eUI`|人間の操作を許可または必要とするマネージクラスおよびメンバーが、部分的に信頼されたコードでの実行をブロックされることを指定します。|  
  
## <a name="remarks"></a>解説  
 [ICLRHostProtectionManager:: SetProtectedCategories](iclrhostprotectionmanager-setprotectedcategories-method.md)メソッドは、型のパラメーターを受け取り `EApiCategories` ます。  
  
 `EApiCategories`列挙体とメソッドは、 `SetProtectedCategories` マネージクラスに直接関連付けられ <xref:System.Security.Permissions.HostProtectionAttribute?displayProperty=nameWithType> ます。 マネージクラスは、値に直接対応する値を持つ列挙体と共に使用され、 <xref:System.Security.Permissions.HostProtectionResource?displayProperty=nameWithType> `EApiCategories` によって記述されたカテゴリに対応する機能を公開するマネージ型およびメンバーをマークし `EApiCategories` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRHostProtectionManager インターフェイス](iclrhostprotectionmanager-interface.md)
- [ホスティングの列挙体](hosting-enumerations.md)
