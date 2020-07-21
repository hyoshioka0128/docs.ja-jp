---
title: EClrFailure 列挙型
ms.date: 03/30/2017
api_name:
- EClrFailure
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrFailure
helpviewer_keywords:
- EClrFailure enumeration [.NET Framework hosting]
ms.assetid: 37b95cce-9bfb-4ecf-a00b-33dcba782c67
topic_type:
- apiref
ms.openlocfilehash: fa2b5052a1d569487f0c6c72699ff9ab571beefc
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504395"
---
# <a name="eclrfailure-enumeration"></a>EClrFailure 列挙型
ホストがポリシーアクションを設定できるエラーのセットについて説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    FAIL_NonCriticalResource,  
    FAIL_CriticalResource,  
    FAIL_FatalRuntime,  
    FAIL_OrphanedLock  
    FAIL_StackOverflow  
    FAIL_AccessViolation  
    FAIL_CodeContract  
} EClrFailure;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`FAIL_NonCriticalResource`|クリティカルでないコード領域に、リソース (スレッド、メモリブロック、ロックなど) を割り当てようとしたときにエラーが発生しました。|  
|`FAIL_CriticalResource`|コードの重要な領域に、リソース (スレッド、メモリブロック、ロックなど) を割り当てようとしたときにエラーが発生しました。|  
|`FAIL_FatalRuntime`|共通言語ランタイム (CLR) は、プロセスでマネージコードを実行できなくなりました。 その後では、任意のホスト関数を呼び出すと、HOST_E_CLRNOTAVAILABLE の HRESULT 値が返されます。|  
|`FAIL_OrphanedLock`|スレッドは、オブジェクトから戻るときにロックを解放できませんでした <xref:System.AppDomain> 。 ホストは、このエラーを設定してスレッドを中止することはできません。|  
|`FAIL_StackOverflow`|スタックオーバーフローが発生しました。|  
|`FAIL_AccessViolation`|保護されたメモリの読み取りまたは書き込みが試行されました。 .NET Framework 4 ではサポートされていません。|  
|`FAIL_CodeContract`|コードコントラクトエラーが発生しました。 「[コードコントラクト](../../debug-trace-profile/code-contracts.md)」を参照してください。|  
  
## <a name="remarks"></a>解説  
 エラー条件のポリシーアクションを指定するためにホストで使用できる[Epolicyaction](epolicyaction-enumeration.md)値の一覧については、 [ICLRPolicyManager:: SetActionOnFailure](iclrpolicymanager-setactiononfailure-method.md)メソッドを参照してください。 クリティカルな、またはクリティカルでないコード領域の詳細については、「 [EClrOperation](eclroperation-enumeration.md)」を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
- [SetActionOnFailure メソッド](iclrpolicymanager-setactiononfailure-method.md)
- [IHostPolicyManager インターフェイス](ihostpolicymanager-interface.md)
- [ホスティングの列挙型](hosting-enumerations.md)
