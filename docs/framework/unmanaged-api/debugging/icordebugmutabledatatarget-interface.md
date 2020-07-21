---
title: ICorDebugMutableDataTarget インターフェイス
ms.date: 03/30/2017
ms.assetid: 14aad5b3-84ab-4bbc-94e3-1eb92e258d10
ms.openlocfilehash: fcf7521f8261c8f8f84c7a9a9deb4b7a7d739c6e
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210008"
---
# <a name="icordebugmutabledatatarget-interface"></a>ICorDebugMutableDataTarget インターフェイス
変更可能なデータターゲットをサポートするために、の機能を拡張[します。](icordebugdatatarget-interface.md)  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ContinueStatusChanged メソッド](icordebugmutabledatatarget-continuestatuschanged-method.md)|指定されたスレッド上の未処理のデバッグ イベントの継続状態を変更します。|  
|[SetThreadContext メソッド](icordebugmutabledatatarget-setthreadcontext-method.md)|スレッドのコンテキスト (レジスタの値) を設定します。|  
|[WriteVirtual メソッド](icordebugmutabledatatarget-writevirtual-method.md)|ターゲット プロセスのアドレス空間にメモリを書き込みます。|  
  
## <a name="remarks"></a>Remarks  
 このモジュール[へのこの](icordebugdatatarget-interface.md)拡張機能は、ターゲットプロセスを変更する (たとえば、ライブによる干渉デバッグを実行する) デバッグツールで実装できます。  
  
 これらのメソッドすべては省略可能です。つまり、このインターフェイスを実装しない場合や、これらのメソッドに対する呼び出しに失敗する場合にも、コア検査に基づくデバッグ機能は失われません。  これらのメソッドからの失敗 `HRESULT` すべては、ICorDebug メソッドからの `HRESULT` として伝達されます。  
  
 1 回の ICorDebug メソッド呼び出しによって複数の変更が行われる可能性があること、および関連する変更をトランザクションごとに適用するメカニズムがないこと (すべてに適用するか、まったく適用しないかのどちらか) に注意してください。  つまり、(同じ ICorDebug 呼び出しの) 他のユーザーが正常に完了した後に変更を失敗すると、ターゲット プロセスは一貫性のない状態のままになり、デバッグが信頼性に欠ける結果になる可能性があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
