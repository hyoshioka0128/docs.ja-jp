---
title: ICorDebugStringValue::GetLength メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugStringValue.GetLength
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStringValue::GetLength
helpviewer_keywords:
- ICorDebugStringValue::GetLength method [.NET Framework debugging]
- GetLength method [.NET Framework debugging]
ms.assetid: a1ebfc69-46a6-4225-8788-b7cfb2f15e1d
topic_type:
- apiref
ms.openlocfilehash: 945e4ac88634c9103a722a180a4fe92a554ca53b
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378895"
---
# <a name="icordebugstringvaluegetlength-method"></a>ICorDebugStringValue::GetLength メソッド
このによって参照される文字列の文字数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetLength (  
    [out] ULONG32   *pcchString  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pcchString`  
 入出力このオブジェクトによって参照される文字列の長さを指定する値へのポインター `ICorDebugStringValue` 。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
