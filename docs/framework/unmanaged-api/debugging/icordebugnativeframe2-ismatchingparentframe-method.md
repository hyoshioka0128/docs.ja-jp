---
title: ICorDebugNativeFrame2::IsMatchingParentFrame メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame2.IsMatchingParentFrame Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame2::IsMatchingParentFrame
helpviewer_keywords:
- IsMatchingParentFrame method [.NET Framework debugging]
- ICorDebugNativeFrame2::IsMatchingParentFrame method [.NET Framework debugging]
ms.assetid: d2ca20db-df22-4528-a0dd-a09ea62c8998
topic_type:
- apiref
ms.openlocfilehash: 5bcced647af6436bd8f5b1f3779d9368b6173d11
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213037"
---
# <a name="icordebugnativeframe2ismatchingparentframe-method"></a>ICorDebugNativeFrame2::IsMatchingParentFrame メソッド
指定したフレームが現在のフレームの親であるかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsMatchingParentFrame([in] ICorDebugNativeFrame2  
                                      *pPotentialParentFrame,  
                              [out] BOOL *pIsParent);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pPotentialParentFrame`  
 から親ステータスとして評価するフレームオブジェクトへのポインター。  
  
 `pIsParent`  
 [出力] `true``pPotentialParentFrame`が現在のフレームの親である場合は。それ以外の場合は `false` 。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|親の状態が正常に返されました。|  
|E_FAIL|親の状態を返すことができませんでした。|  
|E_INVALIDARG|`pPotentialParentFrame` または `pIsParent` が null です。|  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>Remarks  
 `IsMatchingParentFrame``true`メソッドに渡すフレームオブジェクトが、メソッドが呼び出されたフレームオブジェクトの親である場合、を返します。 指定したフレームの子ではないフレームに対してメソッドを呼び出すと、エラーが返されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugNativeFrame2 インターフェイス](icordebugnativeframe2-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
