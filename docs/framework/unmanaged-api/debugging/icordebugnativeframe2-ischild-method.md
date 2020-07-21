---
title: ICorDebugNativeFrame2::IsChild メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame2.IsChild Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame2::IsChild
helpviewer_keywords:
- IsChild method [.NET Framework debugging]
- ICorDebugNativeFrame2::IsChild method [.NET Framework debugging]
ms.assetid: 9e2aae09-49cb-4fbd-81e5-e29cd864a88b
topic_type:
- apiref
ms.openlocfilehash: 759ba7bd46f8231143e743aa5ffcabffeb99c3b6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205110"
---
# <a name="icordebugnativeframe2ischild-method"></a>ICorDebugNativeFrame2::IsChild メソッド
現在のフレームが子フレームであるかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT IsChild([out] BOOL * pIsChild);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pIsChild`  
 入出力現在のフレームが子フレームであるかどうかを指定するブール値。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の特定の HRESULT と、メソッドの失敗を示す HRESULT エラーも返します。  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|子の状態が正常に返されました。|  
|E_FAIL|子の状態を返すことができませんでした。|  
|E_INVALIDARG|`pIsChild` が null です。|  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>Remarks  
 メソッドを `IsChild` `true` 呼び出す frame オブジェクトが別のフレームの子である場合、メソッドはを返します。 この場合は、 [IsMatchingParentFrame](icordebugnativeframe2-ismatchingparentframe-method.md)メソッドを使用して、フレームが親であるかどうかを確認します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugNativeFrame2 インターフェイス](icordebugnativeframe2-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
