---
title: ICorDebugAppDomain2::GetFunctionPointerType メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain2.GetFunctionPointerType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain2::GetFunctionPointerType
helpviewer_keywords:
- ICorDebugAppDomain2::GetFunctionPointerType method [.NET Framework debugging]
- GetFunctionPointerType method [.NET Framework debugging]
ms.assetid: 0aba6096-5b38-435c-a72a-86d35db4daef
topic_type:
- apiref
ms.openlocfilehash: fb9b5ee329b41a8b842b94d59bd61c8bcf5f0bf5
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895148"
---
# <a name="icordebugappdomain2getfunctionpointertype-method"></a>ICorDebugAppDomain2::GetFunctionPointerType メソッド
指定されたシグネチャを持つ関数へのポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFunctionPointerType (  
    [in] ULONG32                             nTypeArgs,  
    [in, size_is(nTypeArgs)] ICorDebugType   *ppTypeArgs[],  
    [out] ICorDebugType                      **ppType  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `nTypeArgs`  
 から関数の型引数の数。  
  
 `ppTypeArgs`  
 からポインターの配列。各ポインターは、関数の型引数を表す、テキスト型のオブジェクトを指します。 最初の要素は戻り値の型です。その他の要素はそれぞれパラメーター型です。  
  
 `ppType`  
 入出力関数へのポインターを表す`ICorDebugType`オブジェクトのアドレスへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
