---
title: ICorDebugModule2 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugModule2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2
helpviewer_keywords:
- ICorDebugModule2 interface [.NET Framework debugging]
ms.assetid: 0847e64f-fdbe-4c96-8168-da20fdc84d80
topic_type:
- apiref
ms.openlocfilehash: 7b98302985d9d54599ea8ea2e01dc2503c468d58
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210229"
---
# <a name="icordebugmodule2-interface"></a>ICorDebugModule2 インターフェイス

モジュールインターフェイスの論理拡張機能として機能します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ApplyChanges メソッド](icordebugmodule2-applychanges-method.md)|メタデータの変更と、Microsoft 中間言語 (MSIL) コードの変更を実行中のプロセスに適用します。|  
|[GetJITCompilerFlags メソッド](icordebugmodule2-getjitcompilerflags-method.md)|このの just-in-time (JIT) コンパイルを制御するフラグを取得し `ICorDebugModule2` ます。|  
|[ResolveAssembly メソッド](icordebugmodule2-resolveassembly-method.md)|指定したメタデータトークンによって参照されるアセンブリを解決します。|  
|[SetJITCompilerFlags メソッド](icordebugmodule2-setjitcompilerflags-method.md)|このの JIT コンパイルを制御するフラグを設定 `ICorDebugModule2` します。|  
|[SetJMCStatus メソッド](icordebugmodule2-setjmcstatus-method.md)|こののすべてのクラスのすべてのメソッドのマイコードのみ (JMC) の状態を、 `ICorDebugModule2` 指定した値に設定し `pTokens` ます。ただし、逆の値に設定されている配列内のすべてのメソッドを除きます。|  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
