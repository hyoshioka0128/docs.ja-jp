---
title: ICorDebugHeapValue インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue
helpviewer_keywords:
- ICorDebugHeapValue interface [.NET Framework debugging]
ms.assetid: 1bca66db-0359-4ae8-846e-e35f7e547e8b
topic_type:
- apiref
ms.openlocfilehash: 36a485413490045ca49b99fca4fe5d43edc37114
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213011"
---
# <a name="icordebugheapvalue-interface"></a>ICorDebugHeapValue インターフェイス

共通言語ランタイム (CLR) ガベージコレクターによって収集されたオブジェクトを表す "ICorDebugValue" のサブクラス。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CreateRelocBreakpoint メソッド](icordebugheapvalue-createrelocbreakpoint-method.md)|実装されていません。|  
|[IsValid メソッド](icordebugheapvalue-isvalid-method.md)|このによって表されるオブジェクトが有効かどうか、 `ICorDebugHeapValue` またはガベージコレクターによって解放されたかどうかを示す値を取得します。 このメソッドは .NET Framework バージョン2.0 では非推奨とされました。|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
