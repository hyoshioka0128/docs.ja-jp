---
title: ISymUnmanagedVariable::GetAttributes メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetAttributes
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetAttributes
helpviewer_keywords:
- GetAttributes method [.NET Framework debugging]
- ISymUnmanagedVariable::GetAttributes method [.NET Framework debugging]
ms.assetid: 80f168af-a6a6-4c8f-b9e6-8a82dc834ed5
topic_type:
- apiref
ms.openlocfilehash: 29869abdd39f61c6c9cb51d6b2be50fa462c5b70
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615255"
---
# <a name="isymunmanagedvariablegetattributes-method"></a>ISymUnmanagedVariable::GetAttributes メソッド
この変数の属性フラグを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAttributes(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力属性を受け取るへのポインター `ULONG32` 。 返される値は、 [Corsymvarflag](corsymvarflag-enumeration.md)列挙で定義されている値のいずれかになります。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedVariable インターフェイス](isymunmanagedvariable-interface.md)
