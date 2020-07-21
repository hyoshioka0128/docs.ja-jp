---
title: ICorDebugAppDomain::GetName メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.GetName
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::GetName
helpviewer_keywords:
- ICorDebugAppDomain::GetName method [.NET Framework debugging]
- GetName method, ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: 02c596d7-00b0-4e2c-856b-5425158fcefd
topic_type:
- apiref
ms.openlocfilehash: 3db37576f5da7b26e7bd9d3343f8bb8b97f2ba82
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895243"
---
# <a name="icordebugappdomaingetname-method"></a>ICorDebugAppDomain::GetName メソッド
アプリケーションドメインの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetName (  
    [in]  ULONG32           cchName,  
    [out] ULONG32           *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]
         WCHAR              szName[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cchName`  
 [in] `szName` 配列のサイズ。 このメソッドをクエリモードにするには、この値を0に設定します。  
  
 `pcchName`  
 入出力名前のサイズ、またはで実際に`szName`返された文字数へのポインター。 クエリモードでは、この値によって、呼び出し元は、名前に割り当てるバッファーの大きさを知ることができます。  
  
 `szName`  
 入出力アプリケーションドメインの名前を格納する配列。  
  
## <a name="remarks"></a>解説  
 デバッガーは、 `GetName`メソッドを1回呼び出して、名前に必要なバッファーのサイズを取得します。 デバッガーによってバッファーが割り当てられ、メソッドが2回目に呼び出されてバッファーに格納されます。 名前のサイズを取得するための最初の呼び出しは、*クエリモード*と呼ばれます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
