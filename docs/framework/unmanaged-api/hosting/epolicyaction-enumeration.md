---
title: EPolicyAction 列挙型
ms.date: 03/30/2017
api_name:
- EPolicyAction
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EPolicyAction
helpviewer_keywords:
- EPolicyAction enumeration [.NET Framework hosting]
ms.assetid: 72dd76ba-239e-45ac-9ded-318fb07d6c6d
topic_type:
- apiref
ms.openlocfilehash: 901c62e6f2519fc4f9251f348c77b11bbe0992be
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504346"
---
# <a name="epolicyaction-enumeration"></a>EPolicyAction 列挙型
[EClrOperation](eclroperation-enumeration.md)によって記述された操作や[eclrfailure](eclrfailure-enumeration.md)によって記述されたエラーについて、ホストが設定できるポリシーアクションについて説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    eNoAction,  
    eThrowException,  
    eAbortThread,  
    eRudeAbortThread,  
    eUnloadAppDomain,  
    eRudeUnloadAppDomain,  
    eExitProcess,  
    eFastExitProcess,  
    eRudeExitProcess,  
    eDisableRuntime  
} EPolicyAction;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`eAbortThread`|共通言語ランタイム (CLR) がスレッドを正常に中止する必要があることを指定します。 正常な中止には、すべて `finally` のブロック、 `catch` スレッドの中止に関連するブロック、およびファイナライザーを実行する試行が含まれます。|  
|`eDisableRuntime`|CLR が無効化された状態になるように指定します。 影響を受けるプロセスでは、それ以上のマネージコードを実行できず、スレッドは CLR への入力がブロックされます。|  
|`eExitProcess`|CLR がプロセスを正常に終了する必要があることを指定します。これには、ファイナライザーの実行やクリーンアップおよびログ操作の実行が含まれます。|  
|`eFastExitProcess`|CLR がファイナライザーを実行したりクリーンアップ操作やログ操作を実行したりせずに、プロセスをすぐに終了するように指定します。 ただし、通知はデバッガーに送信されます。|  
|`eNoAction`|アクションを実行しないことを指定します。|  
|`eRudeAbortThread`|CLR がルースレッド中止を実行することを指定します。 `catch` `finally` でマークされたおよびブロックだけ <xref:System.EnterpriseServices.MustRunInClientContextAttribute> が実行されます。|  
|`eRudeExitProcess`|CLR がファイナライザーまたはログ操作を実行せずにプロセスを終了する必要があることを指定します。|  
|`eRudeUnloadAppDomain`|CLR がのルードアンロードを実行する必要があることを指定し <xref:System.AppDomain> ます。 でマークされたファイナライザーだけ <xref:System.EnterpriseServices.MustRunInClientContextAttribute> が実行されます。 同様に、スタック内のこのを持つすべてのスレッドはを <xref:System.AppDomain> 受け取り `ThreadAbortException` ますが、 `catch` `finally` でマークされたおよびブロックだけ <xref:System.EnterpriseServices.MustRunInClientContextAttribute> が実行されます。|  
|`eThrowException`|メモリ不足、バッファーオーバーフローなどの条件に適した例外をスローする必要があることを指定します。|  
|`eUnloadAppDomain`|をアンロードすることを指定し <xref:System.AppDomain> ます。 CLR はファイナライザーの実行を試みます。|  
  
## <a name="remarks"></a>解説  
 ホストは、 [ICLRPolicyManager](iclrpolicymanager-interface.md)インターフェイスのメソッドを呼び出すことによって、ポリシーアクションを設定します。 ルードと正常な中止の詳細については、 [EClrOperation](eclroperation-enumeration.md)列挙体を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EClrFailure 列挙型](eclrfailure-enumeration.md)
- [ICLRPolicyManager インターフェイス](iclrpolicymanager-interface.md)
- [IHostPolicyManager インターフェイス](ihostpolicymanager-interface.md)
- [ホスティングの列挙型](hosting-enumerations.md)
