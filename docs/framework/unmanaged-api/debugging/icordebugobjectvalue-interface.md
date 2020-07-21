---
title: ICorDebugObjectValue インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue
helpviewer_keywords:
- ICorDebugObjectValue interface [.NET Framework debugging]
ms.assetid: 937de6a0-6fbf-4ddc-80ea-a6217b73e62b
topic_type:
- apiref
ms.openlocfilehash: 603ab20b57dc4ba736b0342797d0be649a5bebc4
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207489"
---
# <a name="icordebugobjectvalue-interface"></a>ICorDebugObjectValue インターフェイス

オブジェクトを含む値を表す "ICorDebugValue" のサブクラス。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetClass メソッド](icordebugobjectvalue-getclass-method.md)|<xref:System.Type>このが参照するオブジェクトの共通言語ランタイム (CLR) へのインターフェイスポインターを取得し `ICorDebugObjectValue` ます。|  
|[GetContext メソッド](icordebugobjectvalue-getcontext-method.md)|実装されていません。|  
|[GetFieldValue メソッド](icordebugobjectvalue-getfieldvalue-method.md)|指定したクラスの指定したフィールドの値を表す、 [ICorDebugValue](icordebugvalue-interface.md)へのインターフェイスポインターを取得します。|  
|[GetManagedCopy メソッド](icordebugobjectvalue-getmanagedcopy-method.md)|互換性のために残されています。 このメソッドは呼び出さないでください。|  
|[GetVirtualMethod メソッド](icordebugobjectvalue-getvirtualmethod-method.md)|実装されていません。|  
|[IsValueClass メソッド](icordebugobjectvalue-isvalueclass-method.md)|このによって参照されるオブジェクトが値型かどうかを示す値を取得し `ICorDebugObjectValue` ます。|  
|[SetFromManagedCopy メソッド](icordebugobjectvalue-setfrommanagedcopy-method.md)|互換性のために残されています。 このメソッドは呼び出さないでください。|  
  
## <a name="remarks"></a>Remarks  
 は、 `ICorDebugObjectValue` デバッグ中のプロセスが続行されるまで有効なままです。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
