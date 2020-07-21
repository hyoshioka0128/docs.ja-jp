---
title: ICLRDebugManager インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRDebugManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDebugManager
helpviewer_keywords:
- ICLRDebugManager interface [.NET Framework hosting]
ms.assetid: e835062c-c7d6-4945-8a44-2de7ebf3928e
topic_type:
- apiref
ms.openlocfilehash: 653c8d1d3edd38e646b4e90c0e48dbe15bed102a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504265"
---
# <a name="iclrdebugmanager-interface"></a>ICLRDebugManager インターフェイス
ホストが一連のタスクを識別子とフレンドリ名に関連付けることができるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[BeginConnection メソッド](iclrdebugmanager-beginconnection-method.md)|ホストとデバッガーの間の新しい接続を確立して、タスクを識別子とフレンドリ名に関連付けます。|  
|[EndConnection メソッド](iclrdebugmanager-endconnection-method.md)|タスクのリストと id とフレンドリ名の間の関連付けを削除します。|  
|[GetDacl メソッド](iclrdebugmanager-getdacl-method.md)|このメソッドは実装されていません。|  
|[IsDebuggerAttached メソッド](iclrdebugmanager-isdebuggerattached-method.md)|デバッガーがプロセスにアタッチされているかどうかを示す値を取得します。|  
|[SetConnectionTasks メソッド](iclrdebugmanager-setconnectiontasks-method.md)|[ICLRTask](iclrtask-interface.md)インスタンスのリストを識別子とフレンドリ名に関連付けます。|  
|[SetDacl メソッド](iclrdebugmanager-setdacl-method.md)|このメソッドは実装されていません。|  
|[SetSymbolReadingPolicy メソッド](iclrdebugmanager-setsymbolreadingpolicy-method.md)|プログラムデータベース (PDB) ファイルを読み取るためのポリシーを設定します。 ポリシーは、行番号とファイルに関する情報が呼び出し履歴に含まれるかどうかを決定します。|  
  
## <a name="remarks"></a>解説  
 デバッグシナリオでは、ホストは、独自のプログラミングロジックに従ってタスクをグループ化することが必要になる場合があります。 たとえば、グループ化により、開発者は、プロセスで実行されているすべてのタスクを表示するのではなく、開発者の Api に必要なタスクのみを参照できます。 `ICLRDebugManager`ホストがこの種のグループ化を実装できるようにします。  
  
> [!IMPORTANT]
> 、 `ICLRDebugManager` `BeginConnection` 、およびの3つのメソッドは相互に `SetConnectionTasks` `EndConnection` 依存しています。 これらは、想定どおりに動作するために、指定された順序で呼び出される必要があります。  
  
 グループ化、およびホストがグループに割り当てる識別子とフレンドリ名は、共通言語ランタイム (CLR) には意味がありません。 CLR は、情報をデバッガーに渡すだけです。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト インターフェイス](hosting-interfaces.md)
