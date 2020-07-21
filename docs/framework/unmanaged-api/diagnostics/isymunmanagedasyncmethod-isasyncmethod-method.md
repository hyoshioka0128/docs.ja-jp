---
title: ISymUnmanagedAsyncMethod::IsAsyncMethod メソッド
ms.date: 03/30/2017
ms.assetid: 670a7653-dac6-4171-98ee-d669e3adf4b2
ms.openlocfilehash: 91b4c2688dadf12fa4a835a662622267d7831cf8
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441800"
---
# <a name="isymunmanagedasyncmethodisasyncmethod-method"></a>ISymUnmanagedAsyncMethod::IsAsyncMethod メソッド
メソッドに非同期情報があるかどうかを確認します。  
  
 このメソッドがを返す場合 `FALSE` 、このインターフェイス内の他のメソッドを呼び出すことはできません。 これらはすべて、 `E_UNEXPECTED` この場合はを返します。  
  
## <a name="syntax"></a>構文  
  
```idl  
HRESULT IsAsyncMethod(    [out, retval] BOOL* pRetVal);  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`pRetVal`||  
  
## <a name="return-value"></a>戻り値  
 `HRESULT` を返します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedAsyncMethod インターフェイス](isymunmanagedasyncmethod-interface.md)
