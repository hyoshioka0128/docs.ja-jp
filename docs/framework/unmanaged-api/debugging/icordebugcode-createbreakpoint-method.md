---
title: ICorDebugCode::CreateBreakpoint メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugCode.CreateBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::CreateBreakpoint
helpviewer_keywords:
- ICorDebugCode::CreateBreakpoint method [.NET Framework debugging]
- CreateBreakpoint method, ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 46842618-0fe4-480b-871c-82fba82d23d9
topic_type:
- apiref
ms.openlocfilehash: 40582b1289875d5151ea96e3153c6e4760737e84
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893806"
---
# <a name="icordebugcodecreatebreakpoint-method"></a>ICorDebugCode::CreateBreakpoint メソッド
このコードセグメントの指定したオフセット位置にブレークポイントを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateBreakpoint (  
    [in] ULONG32     offset,  
    [out] ICorDebugFunctionBreakpoint **ppBreakpoint  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `offset`  
 からブレークポイントを作成する位置のオフセット。  
  
 `ppBreakpoint`  
 入出力ブレークポイントを表す "いいね! ブレークポイント" オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 ブレークポイントがアクティブになる前に、そのブレークポイントをプロセスオブジェクトに追加する必要があります。  
  
 このコードが Microsoft 中間言語 (MSIL) コードで、just-in-time (JIT) でコンパイルされたネイティブバージョンのコードがある場合、ブレークポイントは JIT コンパイルコードにも適用されます。 (コードが後で JIT コンパイルされる場合も同様です)。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
