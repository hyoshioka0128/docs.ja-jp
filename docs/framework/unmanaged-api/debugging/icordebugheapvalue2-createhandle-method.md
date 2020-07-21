---
title: ICorDebugHeapValue2::CreateHandle メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue2.CreateHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue2::CreateHandle
helpviewer_keywords:
- CreateHandle method [.NET Framework debugging]
- ICorDebugHeapValue2::CreateHandle method [.NET Framework debugging]
ms.assetid: fbc418e8-fa22-420d-84ec-e0e1800db041
topic_type:
- apiref
ms.openlocfilehash: cbc056e9a3cc00178b32dee4011da4403dff508a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212777"
---
# <a name="icordebugheapvalue2createhandle-method"></a>ICorDebugHeapValue2::CreateHandle メソッド
この ICorDebugHeapValue2 オブジェクトによって表されるヒープ値に対して指定された型のハンドルを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateHandle (  
    [in] CorDebugHandleType      type,
    [out] ICorDebugHandleValue   **ppHandle  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `type`  
 から作成するハンドルの種類を指定する CorDebugHandleType 列挙体の値。  
  
 `ppHandle`  
 入出力このヒープ値の新しいハンドルを表す、値オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 ハンドルは、ヒープ値に関連付けられているアプリケーションドメインに作成され、アプリケーションドメインがアンロードされると無効になります。  
  
 同じヒープ値に対してこの関数を複数回呼び出すと、複数のハンドルが作成されます。 ハンドルはガベージコレクターのパフォーマンスに影響を与えるため、デバッガーは、一度にアクティブな比較的少数のハンドル (約 256) に制限する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
