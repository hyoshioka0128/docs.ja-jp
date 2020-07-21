---
title: ICorDebugRegisterSet インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugRegisterSet
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugRegisterSet
helpviewer_keywords:
- ICorDebugRegisterSet interface [.NET Framework debugging]
ms.assetid: d3d9676d-0b87-4bc3-b679-7bbc7a186c88
topic_type:
- apiref
ms.openlocfilehash: 7c60fa775b82372b50d1eb3891f107b97df3e73a
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378266"
---
# <a name="icordebugregisterset-interface"></a>ICorDebugRegisterSet インターフェイス
現在コードを実行しているコンピューターで使用できるレジスタのセットを表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetRegisters メソッド](icordebugregisterset-getregisters-method.md)|ビットマスクによって指定された、(現在コードを実行しているコンピューター上の) 各レジスタの値を取得します。|  
|[GetRegistersAvailable メソッド](icordebugregisterset-getregistersavailable-method.md)|現在使用できるレジスタを示すビットマスクを取得し `ICorDebugRegisterSet` ます。|  
|[GetThreadContext メソッド](icordebugregisterset-getthreadcontext-method.md)|現在のスレッドのコンテキストを取得します。|  
|[SetRegisters メソッド](icordebugregisterset-setregisters-method.md)|.NET Framework バージョン2.0 には実装されていません。|  
|[SetThreadContext メソッド](icordebugregisterset-setthreadcontext-method.md)|.NET Framework 2.0 には実装されていません。|  
  
## <a name="remarks"></a>Remarks  
 インターフェイスでは、 `ICorDebugRegisterSet` 32 ビットレジスタのみがサポートされます。 追加のレジスタを必要とする IA-64 などのプラットフォームで[ICorDebugRegisterSet2](icordebugregisterset2-interface.md)インターフェイスを使用します。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [ICorDebugRegisterSet2 インターフェイス](icordebugregisterset2-interface.md)
