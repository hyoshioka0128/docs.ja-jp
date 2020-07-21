---
title: ICLRTask2::EndPreventAsyncAbort メソッド
ms.date: 03/30/2017
api_name:
- ICLRTask2.EndPreventAsyncAbort
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2::EndPreventAsyncAbort
helpviewer_keywords:
- EndPreventAsyncAbort method [.NET Framework hosting]
- ICLRTask2::EndPreventAsyncAbort method [.NET Framework hosting]
ms.assetid: d8013659-e3df-44b3-814f-a6b534ce62f8
topic_type:
- apiref
ms.openlocfilehash: 3ea36c56ef9ccf5886ba96191627e5283da186f7
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762854"
---
# <a name="iclrtask2endpreventasyncabort-method"></a>ICLRTask2::EndPreventAsyncAbort メソッド
新しいまたは保留中のスレッド中止要求に対して、現在のスレッドでのスレッドの中止を許可します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EndPreventAsyncAbort();  
```  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|HOST_E_INVALIDOPERATION|メソッドは、現在のスレッドではないスレッドで呼び出されました。|  
  
## <a name="remarks"></a>解説  
 このメソッドを呼び出すと、現在のスレッドの遅延スレッド中止カウンターが1つ減少します。  
  
 [ICLRTask2:: BeginPreventAsyncAbort](iclrtask2-beginpreventasyncabort-method.md)の呼び出しと `EndPreventAsyncAbort` 入れ子にすることができます。 カウンターがゼロより大きい限り、現在のスレッドのスレッド中止は遅延されます。  
  
 この機能によって公開されている機能は、仮想マシン (VM) によって内部的に使用されます。 これらの方法を誤用すると、VM で特定できない動作が発生する可能性があります。 たとえば、最初に `EndPreventAsyncAbort` を呼び出しないでを呼び出す `BeginPreventAsyncAbort` と、VM で以前にインクリメントしたカウンターが0に設定されます。 同様に、内部カウンターのオーバーフローはチェックされません。 ホストと VM の両方によってインクリメントされるために整数の制限を超えた場合、結果として得られる動作は指定されません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [BeginPreventAsyncAbort メソッド](iclrtask2-beginpreventasyncabort-method.md)
- [ICLRTask2 インターフェイス](iclrtask2-interface.md)
- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
