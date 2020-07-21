---
title: ISymUnmanagedWriter::DefineLocalVariable メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineLocalVariable
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineLocalVariable
helpviewer_keywords:
- ISymUnmanagedWriter::DefineLocalVariable method [.NET Framework debugging]
- DefineLocalVariable method [.NET Framework debugging]
ms.assetid: 6fab8a58-3883-490f-8b27-64042c90f104
topic_type:
- apiref
ms.openlocfilehash: 5730cdd910257d762230f5e54576d5e0a7ac1adb
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614826"
---
# <a name="isymunmanagedwriterdefinelocalvariable-method"></a>ISymUnmanagedWriter::DefineLocalVariable メソッド
現在の構文のスコープの変数を 1 つ定義します。 このメソッドは、スコープ全体で複数のホームを持つ同じ名前の変数に対して複数回呼び出すことができます。 ただし、この場合は、 `startOffset` パラメーターとパラメーターの値 `endOffset` が重複していてはなりません。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineLocalVariable(  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] ULONG32      cSig,  
    [in, size_is(cSig)] unsigned char signature[],  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3,  
    [in] ULONG32      startOffset,  
    [in] ULONG32      endOffset);  
```  
  
## <a name="parameters"></a>パラメーター  
 `name`  
 から`WCHAR`ローカル変数名を定義するへのポインター。  
  
 `attributes`  
 からローカル変数の属性。  
  
 `cSig`  
 から`ULONG32`バッファーのサイズ (バイト単位) を示す `signature` 。  
  
 `signature`  
 からローカル変数シグネチャ。  
  
 `addrKind`  
 からアドレスの種類。  
  
 `addr1`  
 からパラメーター指定の最初のアドレス。  
  
 `addr2`  
 からパラメーター指定の2番目のアドレス。  
  
 `addr3`  
 からパラメーター指定の3番目のアドレス。  
  
 `startOffset`  
 から変数の開始オフセット。 このパラメーターは省略可能です。 0の場合、このパラメーターは無視され、スコープ全体にわたって変数が定義されます。 0以外の値の場合、変数は現在のスコープのオフセット内になります。  
  
 `endOffset`  
 から変数の終了オフセット。 このパラメーターは省略可能です。 0の場合、このパラメーターは無視され、スコープ全体にわたって変数が定義されます。 0以外の値の場合、変数は現在のスコープのオフセット内になります。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
- [DefineGlobalVariable メソッド](isymunmanagedwriter-defineglobalvariable-method.md)
- [DefineLocalVariable2 メソッド](isymunmanagedwriter2-definelocalvariable2-method.md)
