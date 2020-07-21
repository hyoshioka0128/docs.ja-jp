---
title: ICorDebugAssembly2::IsFullyTrusted メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugAssembly2.IsFullyTrusted
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAssembly2::IsFullyTrusted
helpviewer_keywords:
- ICorDebugAssembly2::IsFullyTrusted method [.NET Framework debugging]
- IsFullyTrusted method [.NET Framework debugging]
ms.assetid: 26cbd27d-12bf-444a-8197-ccd14d37dda3
topic_type:
- apiref
ms.openlocfilehash: dd82709064fe7f7d912d93f4b3f0248769f02b9e
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894882"
---
# <a name="icordebugassembly2isfullytrusted-method"></a>ICorDebugAssembly2::IsFullyTrusted メソッド
アセンブリにランタイムセキュリティシステムによる完全信頼が付与されているかどうかを示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsFullyTrusted(  
    [out] BOOL *pbFullyTrusted  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbFullyTrusted`  
 入出力`true`アセンブリにランタイムセキュリティシステムによる完全信頼が付与されている場合は。それ以外`false`の場合は。  
  
## <a name="remarks"></a>解説  
 このメソッドは、アセンブリのセキュリティポリシーがまだ解決されていない場合、つまりアセンブリ内のコードがまだ実行されていない場合に、CORDBG_E_NOTREADY の HRESULT を返します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
