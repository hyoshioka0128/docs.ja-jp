---
title: ICorDebugILFrame2::RemapFunction メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame2.RemapFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame2::RemapFunction
helpviewer_keywords:
- ICorDebugILFrame2::RemapFunction method [.NET Framework debugging]
- RemapFunction method [.NET Framework debugging]
ms.assetid: dd639ba0-f77b-426d-9ff6-f92706840348
topic_type:
- apiref
ms.openlocfilehash: 43f585417ed52b92c23087c0f02fd188ee09ea7e
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210216"
---
# <a name="icordebugilframe2remapfunction-method"></a>ICorDebugILFrame2::RemapFunction メソッド
新しい Microsoft 中間言語 (MSIL) オフセットを指定して、編集された関数を再マップします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RemapFunction (  
    [in] ULONG32      newILOffset  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `newILOffset`  
 から命令ポインターが配置されるスタックフレームの新しい MSIL オフセット。 この値は、シーケンスポイントである必要があります。  
  
 この値の有効性を保証するのは、呼び出し元の責任です。 たとえば、関数の境界の外側にある場合、MSIL オフセットは無効です。  
  
## <a name="remarks"></a>Remarks  
 フレームの関数が編集されると、デバッガーはメソッドを呼び出して、 `RemapFunction` 最後のバージョンのフレームの関数をスワップして実行できるようになります。 コードの実行は、指定された MSIL オフセットから開始されます。  
  
> [!NOTE]
> を呼び出すと (例: `RemapFunction` を[呼び出す](icordebugilframe-setip-method.md)と、スレッドのスタックトレースの生成に関連するすべてのデバッグインターフェイスが無効になります)。 これらのインターフェイス[には](icordebugchain-interface.md)、次のようなインターフェイスがあります。  
  
 メソッドは、 `RemapFunction` 現在のフレームのコンテキストでのみ呼び出すことができ、次のいずれかの場合にのみ呼び出すことができます。  
  
- まだ継続していない[ICorDebugManagedCallback2:: FunctionRemapOpportunity](icordebugmanagedcallback2-functionremapopportunity-method.md)コールバックを受信した後。  
  
- このフレームに対して、コードの実行が停止している間に、このフレームに対しては、[というエラーが発生し](icordebugmanagedcallback-editandcontinueremap-method.md)ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
