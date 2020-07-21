---
title: ICorDebugModule::GetBaseAddress メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugModule.GetBaseAddress
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::GetBaseAddress
helpviewer_keywords:
- GetBaseAddress method [.NET Framework debugging]
- ICorDebugModule::GetBaseAddress method [.NET Framework debugging]
ms.assetid: 26a82815-1982-4eb7-92d1-5c3d318d5be4
topic_type:
- apiref
ms.openlocfilehash: 9270afa1d8c8ddd74cfe6dd05e39c1480f5767e6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83206944"
---
# <a name="icordebugmodulegetbaseaddress-method"></a>ICorDebugModule::GetBaseAddress メソッド
モジュールのベースアドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetBaseAddress(  
    [out] CORDB_ADDRESS *pAddress  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAddress`  
 入出力`CORDB_ADDRESS`モジュールのベースアドレスを指定する。  
  
## <a name="remarks"></a>Remarks  
 モジュールがネイティブイメージの場合 (つまり、モジュールがネイティブイメージジェネレーター Ngen.exe によって生成された場合)、そのベースアドレスはゼロになります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
