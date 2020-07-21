---
title: ISymUnmanagedVariable::GetAddressField1 メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetAddressField1
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetAddressField1
helpviewer_keywords:
- GetAddressField1 method [.NET Framework debugging]
- ISymUnmanagedVariable::GetAddressField1 method [.NET Framework debugging]
ms.assetid: 25788ed1-0ce3-4b97-96fc-88f8997812a3
topic_type:
- apiref
ms.openlocfilehash: 253fd17178c03bc0c4d8ea031888a404ad56f876
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615281"
---
# <a name="isymunmanagedvariablegetaddressfield1-method"></a>ISymUnmanagedVariable::GetAddressField1 メソッド
この変数の最初のアドレスフィールドを取得します。 その意味は、アドレスの種類によって異なります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAddressField1(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力最初のアドレスフィールドを受け取るへのポインター `ULONG32` 。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedVariable インターフェイス](isymunmanagedvariable-interface.md)
- [GetAddressField2 メソッド](isymunmanagedvariable-getaddressfield2-method.md)
- [GetAddressField3 メソッド](isymunmanagedvariable-getaddressfield3-method.md)
- [GetAddressKind メソッド](isymunmanagedvariable-getaddresskind-method.md)
