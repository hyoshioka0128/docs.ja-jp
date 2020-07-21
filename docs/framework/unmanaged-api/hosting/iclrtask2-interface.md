---
title: ICLRTask2 インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRTask2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2
helpviewer_keywords:
- ICLRTask2 interface [.NET Framework hosting]
ms.assetid: b5a22ebc-0582-49de-91f9-97a3d9789290
topic_type:
- apiref
ms.openlocfilehash: b067ca72e030bce24a7efde5e3488a00024e9613
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762868"
---
# <a name="iclrtask2-interface"></a>ICLRTask2 インターフェイス
には、 [ICLRTask](iclrtask-interface.md)インターフェイスのすべての機能が用意されています。また、には、現在のスレッドでスレッドの中止を遅延させることができるメソッドが用意されています。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[BeginPreventAsyncAbort メソッド](iclrtask2-beginpreventasyncabort-method.md)|現在のスレッドの新しいスレッド中止要求を遅延します。|  
|[EndPreventAsyncAbort メソッド](iclrtask2-endpreventasyncabort-method.md)|新しいまたは保留中のスレッド中止要求に対して、現在のスレッドでのスレッドの中止を許可します。|  
  
## <a name="remarks"></a>解説  
 インターフェイスは、 `ICLRTask2` インターフェイスを継承 `ICLRTask` し、ホストがスレッドの中止を遅らせて、失敗しないコードの領域を保護できるようにするメソッドを追加します。 を呼び出す `BeginPreventAsyncAbort` と、現在のスレッドの遅延スレッド中止カウンターがインクリメントされ、を呼び出すと、 `EndPreventAsyncAbort` そのカウンターがデクリメントされます。 およびへの呼び出しは入れ子にする `BeginPreventAsyncAbort` `EndPreventAsyncAbort` ことができます。 カウンターがゼロより大きい限り、現在のスレッドのスレッド中止は遅延されます。  
  
 との呼び出し `BeginPreventAsyncAbort` がペアになって `EndPreventAsyncAbort` いない場合、現在のスレッドにスレッド中止を配信できない状態になる可能性があります。  
  
 遅延は、それ自体を中止するスレッドには適用されません。  
  
 この機能によって公開されている機能は、仮想マシン (VM) によって内部的に使用されます。 これらの方法を誤用すると、VM で特定できない動作が発生する可能性があります。 たとえば、最初に `EndPreventAsyncAbort` を呼び出しないでを呼び出す `BeginPreventAsyncAbort` と、VM で以前にインクリメントしたカウンターが0に設定されます。 同様に、内部カウンターのオーバーフローはチェックされません。 ホストと VM の両方によってインクリメントされるために整数の制限を超えた場合、結果として得られる動作は指定されません。  
  
 から継承されたメンバー `ICLRTask` と、このインターフェイスの他の用途については、「 [ICLRTask](iclrtask-interface.md)インターフェイス」を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRTask インターフェイス](iclrtask-interface.md)
- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
