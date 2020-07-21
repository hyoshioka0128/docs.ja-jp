---
title: ICorDebugClass2 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugClass2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass2
helpviewer_keywords:
- ICorDebugClass2 interface [.NET Framework debugging]
ms.assetid: 5416de70-43f2-4cdf-a11f-d570759c9c0c
topic_type:
- apiref
ms.openlocfilehash: ff15297eb479f7474c9f07123a29263fb4da3205
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893973"
---
# <a name="icordebugclass2-interface"></a>ICorDebugClass2 インターフェイス

ジェネリック、または <xref:System.Type> 型のメソッド パラメーターを持つクラスを表します。 このインターフェイスは[、を](icordebugclass-interface.md)拡張します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetParameterizedType メソッド](icordebugclass2-getparameterizedtype-method.md)|このクラスの型宣言を取得します。|  
|[SetJMCStatus メソッド](icordebugclass2-setjmcstatus-method.md)|このクラスの各メソッドについて、メソッドがユーザー定義のコードかどうかを示す値を設定します。|  
  
## <a name="remarks"></a>解説  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugClass インターフェイス](icordebugclass-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
