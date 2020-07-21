---
title: ISymUnmanagedScope::GetChildren メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope.GetChildren
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope::GetChildren
helpviewer_keywords:
- ISymUnmanagedScope::GetChildren method [.NET Framework debugging]
- GetChildren method [.NET Framework debugging]
ms.assetid: 0bed524e-cc48-4bf0-b9fa-25d665e63ddb
topic_type:
- apiref
ms.openlocfilehash: c6d21f40c260890c9c88dcdfccd7e31161024ba3
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614865"
---
# <a name="isymunmanagedscopegetchildren-method"></a>ISymUnmanagedScope::GetChildren メソッド
このスコープの子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetChildren(  
    [in]  ULONG32  cChildren,  
    [out] ULONG32  *pcChildren,  
    [out, size_is(cChildren),  
        length_is(*pcChildren)] ISymUnmanagedScope* children[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cChildren`  
 から`ULONG32`配列のサイズを示す `children` 。  
  
 `pcChildren`  
 入出力`ULONG32`子を格納するために必要なバッファーのサイズを受け取るへのポインター。  
  
 `children`  
 入出力返された子の配列。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedScope インターフェイス](isymunmanagedscope-interface.md)
- [GetParent メソッド](isymunmanagedscope-getparent-method.md)
