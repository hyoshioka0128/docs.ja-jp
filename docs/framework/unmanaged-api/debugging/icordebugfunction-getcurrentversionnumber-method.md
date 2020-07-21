---
title: ICorDebugFunction::GetCurrentVersionNumber メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugFunction.GetCurrentVersionNumber
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction::GetCurrentVersionNumber
helpviewer_keywords:
- GetCurrentVersionNumber method [.NET Framework debugging]
- ICorDebugFunction::GetCurrentVersionNumber method [.NET Framework debugging]
ms.assetid: c3af1575-cbe6-457a-bc08-c53460edcbc8
topic_type:
- apiref
ms.openlocfilehash: b47580022b98ea02584a94b3f74b3fd1c276f297
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212907"
---
# <a name="icordebugfunctiongetcurrentversionnumber-method"></a>ICorDebugFunction::GetCurrentVersionNumber メソッド
このオブジェクトによって表される関数に対して行われた最新の編集のバージョン番号を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCurrentVersionNumber (  
    [out] ULONG32 *pnCurrentVersion  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pnCurrentVersion`  
 入出力この関数に対して行われた最新の編集のバージョン番号を表す整数値へのポインター。  
  
## <a name="remarks"></a>Remarks  
 この関数に対して行われた最新の編集のバージョン番号が、関数自体のバージョン番号よりも大きい可能性があります。 [ICorDebugFunction2:: GetVersionNumber](icordebugfunction2-getversionnumber-method.md)メソッドまたは[Code:: GetVersionNumber](icordebugcode-getversionnumber-method.md)メソッドを使用して、関数のバージョン番号を取得します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
