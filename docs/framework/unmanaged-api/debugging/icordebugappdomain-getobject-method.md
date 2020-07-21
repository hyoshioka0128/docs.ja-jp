---
title: ICorDebugAppDomain::GetObject メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain.GetObject
api_location:
- corguids.lib
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain::GetObject
helpviewer_keywords:
- ICorDebugAppDomain::GetObject method [.NET Framework debugging]
- GetObject method, ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: 78232e6f-ae18-4cfa-a6cd-e79471cf9d76
topic_type:
- apiref
ms.openlocfilehash: a21f3b36e418bbde5dcb90f25a39dae03fde77c9
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895207"
---
# <a name="icordebugappdomaingetobject-method"></a>ICorDebugAppDomain::GetObject メソッド
共通言語ランタイム (CLR) アプリケーションドメインへのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetObject (  
    [out] ICorDebugValue   **ppObject  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppObject`  
 入出力CLR アプリケーションドメインを表す ICorDebugValue インターフェイスオブジェクトのアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このアプリケーションドメイン<xref:System.AppDomain?displayProperty=nameWithType>に対してマネージオブジェクトが構築されていない`S_FALSE`場合、 `NULL`メソッド`*ppObject`はを返し、をに配置します。  
  
## <a name="remarks"></a>解説  
 プロセス内の各アプリケーションドメインは、それを<xref:System.AppDomain?displayProperty=nameWithType>表すランタイムにマネージオブジェクトを持つことができます。 この関数は、このマネージ<xref:System.AppDomain?displayProperty=nameWithType>オブジェクトに対応する ICorDebugValue インターフェイスオブジェクトを取得します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]
