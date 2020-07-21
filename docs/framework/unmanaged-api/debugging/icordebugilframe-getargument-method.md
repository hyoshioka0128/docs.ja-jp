---
title: ICorDebugILFrame::GetArgument メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.GetArgument
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::GetArgument
helpviewer_keywords:
- GetArgument method [.NET Framework debugging]
- ICorDebugILFrame::GetArgument method [.NET Framework debugging]
ms.assetid: 4e2fd423-f643-4c27-ba5f-41b5ebc3b416
topic_type:
- apiref
ms.openlocfilehash: d715f5842bb7f75da5311d34bf7d4596f0801a92
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210281"
---
# <a name="icordebugilframegetargument-method"></a>ICorDebugILFrame::GetArgument メソッド
この MSIL (Microsoft 中間言語) スタックフレーム内の指定された引数の値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetArgument (  
    [in] DWORD                  dwIndex,  
    [out] ICorDebugValue        **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwIndex`  
 からこの MSIL スタックフレーム内の引数のインデックス。  
  
 `ppValue`  
 [out] 取得した値を表す ICorDebugValue オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 メソッドは、 `GetArgument` MSIL スタックフレーム内または just-in-time (JIT) コンパイルフレームで使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
