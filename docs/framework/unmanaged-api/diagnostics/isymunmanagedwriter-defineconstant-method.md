---
title: ISymUnmanagedWriter::DefineConstant メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineConstant
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineConstant
helpviewer_keywords:
- DefineConstant method [.NET Framework debugging]
- ISymUnmanagedWriter::DefineConstant method [.NET Framework debugging]
ms.assetid: 9e986986-2223-4d5f-b040-85d716146924
topic_type:
- apiref
ms.openlocfilehash: 200e68abb3f176c267045bf2a5e7e35d18400519
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610094"
---
# <a name="isymunmanagedwriterdefineconstant-method"></a>ISymUnmanagedWriter::DefineConstant メソッド
定数値の名前を定義します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineConstant(  
    [in] const WCHAR *name,  
    [in] VARIANT value,  
    [in] ULONG32 cSig,  
    [in, size_is(cSig)] unsigned char signature[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `name`  
 から`WCHAR`定数名を定義するへのポインター。  
  
 `value`  
 から定数の値。  
  
 `cSig`  
 [in] `signature` 配列のサイズ。  
  
 `signature`  
 から定数の型シグネチャ。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
- [DefineConstant2 メソッド](isymunmanagedwriter2-defineconstant2-method.md)
