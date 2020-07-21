---
title: ICorDebugILFrame::EnumerateArguments メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.EnumerateArguments
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::EnumerateArguments
helpviewer_keywords:
- ICorDebugILFrame::EnumerateArguments method [.NET Framework debugging]
- EnumerateArguments method [.NET Framework debugging]
ms.assetid: 00ac81e2-a774-422a-bd88-54a4b3c99f73
topic_type:
- apiref
ms.openlocfilehash: 3945b1dea62dc0616d669356faf60f0d09cfb084
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210307"
---
# <a name="icordebugilframeenumeratearguments-method"></a>ICorDebugILFrame::EnumerateArguments メソッド
このフレーム内の引数の列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumerateArguments (  
    [out] ICorDebugValueEnum    **ppValueEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppValueEnum`  
 入出力このフレーム内の引数の列挙子である、の各オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 `EnumerateArguments`このテキストボックスオブジェクトで表される呼び出しフレームで使用可能な引数を一覧表示できる列挙子を取得します。 この一覧には、 [vararg](/cpp/windows/vararg)である引数 (可変個の引数) と、ではない引数が含まれ `vararg` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
