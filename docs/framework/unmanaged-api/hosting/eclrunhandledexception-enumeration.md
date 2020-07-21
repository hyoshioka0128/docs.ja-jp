---
title: EClrUnhandledException 列挙型
ms.date: 03/30/2017
api_name:
- EClrUnhandledException
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrUnhandledException
helpviewer_keywords:
- EClrUnhandledException enumeration [.NET Framework hosting]
ms.assetid: d231044e-2b53-4836-93f9-8117ff0e5c3a
topic_type:
- apiref
ms.openlocfilehash: 63b07dda2293d3e05bd3c8fcdc45f20a498ea54c
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616308"
---
# <a name="eclrunhandledexception-enumeration"></a>EClrUnhandledException 列挙型
ユーザーコードで処理されない例外を管理するために使用できるオプションについて説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    eRuntimeDeterminedPolicy,  
    eHostDeterminedPolicy  
} EClrUnhandledException;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`eRuntimeDeterminedPolicy`|既定の動作を実行することを指定します。 プロセスが破棄されます。|  
|`eHostDeterminedPolicy`|共通言語ランタイム (CLR) が未処理の例外を無視し、ホストがそれ以上のアクションを決定できるように指定します。|  
  
## <a name="remarks"></a>解説  
 CLR が以前のバージョンと同じように動作するように指定するには、メンバーを使用し `eHostDeterminedPolicy` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrFailure 列挙型](eclrfailure-enumeration.md)
- [EClrOperation 列挙型](eclroperation-enumeration.md)
- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
- [SetUnhandledExceptionPolicy メソッド](iclrpolicymanager-setunhandledexceptionpolicy-method.md)
- [IHostPolicyManager インターフェイス](ihostpolicymanager-interface.md)
- [ホスティングの列挙体](hosting-enumerations.md)
