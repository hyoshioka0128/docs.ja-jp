---
title: EClrEvent 列挙型
ms.date: 03/30/2017
api_name:
- EClrEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- EClrEvent
helpviewer_keywords:
- EClrEvent enumeration [.NET Framework hosting]
ms.assetid: 7c36a7c2-75a2-4971-bc23-abf54c812154
topic_type:
- apiref
ms.openlocfilehash: 3ecaebb9d943a3cdbb231307012b5dc3aaf000f7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84493417"
---
# <a name="eclrevent-enumeration"></a>EClrEvent 列挙型
ホストがコールバックを登録できる共通言語ランタイム (CLR) イベントについて説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    Event_ClrDisabled,  
    Event_DomainUnload,  
    Event_MDAFired,  
    Event_StackOverflow  
} EClrEvent;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`Event_ClrDisabled`|致命的な CLR エラーを指定します。|  
|`Event_DomainUnload`|特定ののアンロードを指定し <xref:System.AppDomain> ます。|  
|`Event_MDAFired`|マネージデバッグアシスタント (MDA) メッセージが生成されたことを示します。|  
|`Event_StackOverflow`|スタックオーバーフローエラーが発生したことを示します。|  
  
## <a name="remarks"></a>解説  
 ホストは、 `EClrEvent` [ICLROnEventManager](iclroneventmanager-interface.md)インターフェイスのメソッドを呼び出すことによって、によって記述された任意のイベントの種類のコールバックを登録できます。 ホストは、 [ICLRControl:: GetCLRManager](iclrcontrol-getclrmanager-method.md)メソッドを呼び出すことによって、このインターフェイスへのポインターを取得します。  
  
 `Event_CLRDisabled`イベントと `Event_DomainUnload` イベントが複数回発生する可能性があり、異なるスレッドから、アンロードまたは CLR の無効化を通知することができます。  
  
 イベントは、 `Event_MDAFired` MDA メッセージの詳細を含む[MDAInfo](mdainfo-structure.md)インスタンスの作成を発生させます。 Mda の詳細については、「[マネージデバッグアシスタントによるエラーの診断](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)」を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [IActionOnCLREvent インターフェイス](iactiononclrevent-interface.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ホスティングの列挙型](hosting-enumerations.md)
