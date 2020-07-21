---
title: ICorDebugModule3 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugModule3
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule3
helpviewer_keywords:
- ICorDebugModule3 interface [.NET Framework debugging]
ms.assetid: 0b69f945-263a-4e11-8512-89d27f6ea296
topic_type:
- apiref
ms.openlocfilehash: 69fd3e2df4a4eafe91cc025f28e1387cc443ea04
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212309"
---
# <a name="icordebugmodule3-interface"></a>ICorDebugModule3 インターフェイス
動的モジュールのシンボル リーダーを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
interface ICorDebugModule3 : IUnknown  
{  
    HRESULT CreateReaderForInMemorySymbols  
      (  
      [in] REFIID riid,  
      [out][iid_is(riid)] void **  ppObj  
      );  
};  
```  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ICorDebugModule3::CreateReaderForInMemorySymbols メソッド](icordebugmodule3-createreaderforinmemorysymbols-method.md)|動的モジュールのシンボルリーダー (通常は[ISymUnmanagedReader インターフェイス](../diagnostics/isymunmanagedreader-interface.md)) を作成します。|  
  
## <a name="remarks"></a>Remarks  
 このインターフェイスは、"ICorDebugModule2" インターフェイスと "" インターフェイスを論理的に拡張します。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** 4.5、4、3.5 SP1
  
## <a name="see-also"></a>関連項目

- [ICorDebugRemoteTarget インターフェイス](icordebugremotetarget-interface.md)
- [ICorDebug インターフェイス](icordebug-interface.md)

- [デバッグのインターフェイス](debugging-interfaces.md)
