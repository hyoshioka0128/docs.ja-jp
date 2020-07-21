---
title: ISymUnmanagedNamespace::GetName メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedNamespace.GetName
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedNamespace::GetName
helpviewer_keywords:
- ISymUnmanagedNamespace::GetName method [.NET Framework debugging]
- GetName method, ISymUnmanagedNamespace interface [.NET Framework debugging]
ms.assetid: 657bf91d-005a-4ea4-9298-04d1291c0bc3
topic_type:
- apiref
ms.openlocfilehash: 84b2f1226c84713483499c7ff777838058cb0f95
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615112"
---
# <a name="isymunmanagednamespacegetname-method"></a>ISymUnmanagedNamespace::GetName メソッド
この名前空間の名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetName(  
    [in]  ULONG32  cchName,  
    [out] ULONG32  *pcchName,  
    [out, size_is(cchName),  
        length_is(*pcchName)] WCHAR szName[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cchName`  
 から`ULONG32`バッファーのサイズを示す `szName` 。  
  
 `pcchName`  
 入出力`ULONG32`Null 終了を含む、名前空間の名前を格納するために必要なバッファーのサイズ (文字数) を受け取るへのポインター。  
  
 `szName`  
 入出力名前空間の名前を格納しているバッファーへのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedNamespace インターフェイス](isymunmanagednamespace-interface.md)
