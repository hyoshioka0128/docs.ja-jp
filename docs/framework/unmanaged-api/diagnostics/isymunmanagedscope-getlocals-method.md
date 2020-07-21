---
title: ISymUnmanagedScope::GetLocals メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope.GetLocals
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope::GetLocals
helpviewer_keywords:
- GetLocals method [.NET Framework debugging]
- ISymUnmanagedScope::GetLocals method [.NET Framework debugging]
ms.assetid: 17c45f15-8c44-44da-b070-f902077b36e4
topic_type:
- apiref
ms.openlocfilehash: 0acd31d85504688427cace0222a657885035c537
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615385"
---
# <a name="isymunmanagedscopegetlocals-method"></a>ISymUnmanagedScope::GetLocals メソッド
このスコープ内で定義されているローカル変数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetLocals(  
    [in]  ULONG32  cLocals,  
    [out] ULONG32  *pcLocals,  
    [out, size_is(cLocals),  
        length_is(*pcLocals)] ISymUnmanagedVariable* locals[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cLocals`  
 から`ULONG32`配列のサイズを示す `locals` 。  
  
 `pcLocals`  
 入出力`ULONG32`ローカル変数を格納するために必要なバッファーのサイズを受け取るへのポインター。  
  
 `locals`  
 入出力ローカル変数を受け取る配列。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedScope インターフェイス](isymunmanagedscope-interface.md)
