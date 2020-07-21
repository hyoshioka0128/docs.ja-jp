---
title: ICorDebugFunction2 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugFunction2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction2
helpviewer_keywords:
- ICorDebugFunction2 interface [.NET Framework debugging]
ms.assetid: 2b936bef-9b75-48bf-859f-42e419c65f1c
topic_type:
- apiref
ms.openlocfilehash: 611091d39da6d7f646457457f20ce1eaf37db361
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213206"
---
# <a name="icordebugfunction2-interface"></a>ICorDebugFunction2 インターフェイス

マイコードのみのステップスルーデバッグをサポートするように、この関数インターフェイスを論理的に拡張します。これにより、非ユーザーコードがスキップされます。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumerateNativeCode メソッド](icordebugfunction2-enumeratenativecode-method.md)|(実装されていません。)この ICorDebugFunction2 オブジェクトによって参照されている関数内のネイティブコードステートメントを含む、コードの型の列挙体へのインターフェイスポインターを取得します。|  
|[GetJMCStatus メソッド](icordebugfunction2-getjmcstatus-method.md)|この関数がユーザーコードとしてマークされているかどうかを示す値を取得します。|  
|[GetVersionNumber メソッド](icordebugfunction2-getversionnumber-method.md)|この関数のエディットコンティニュバージョンを取得します。|  
|[SetJMCStatus メソッド](icordebugfunction2-setjmcstatus-method.md)|マイコードのみのステップ実行のために、この関数をマークします。|  
  
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
