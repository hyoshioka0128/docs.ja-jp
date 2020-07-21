---
title: ISymUnmanagedReader::GetMethodsFromDocumentPosition メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetMethodsFromDocumentPosition
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetMethodsFromDocumentPosition
helpviewer_keywords:
- GetMethodsFromDocumentPosition method [.NET Framework debugging]
- ISymUnmanagedReader::GetMethodsFromDocumentPosition method [.NET Framework debugging]
ms.assetid: 83605f1e-e4f3-49e6-859b-f13cad68bb54
topic_type:
- apiref
ms.openlocfilehash: bba0fc039c403d45e8a5b60f2b0231eb24226280
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614956"
---
# <a name="isymunmanagedreadergetmethodsfromdocumentposition-method"></a>ISymUnmanagedReader::GetMethodsFromDocumentPosition メソッド
メソッドの配列を返します。各メソッドには、ドキュメント内の指定された位置にあるブレークポイントが含まれています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMethodsFromDocumentPosition (  
    [in]  ISymUnmanagedDocument* document,  
    [in]  ULONG32 line,  
    [in]  ULONG32 column,  
    [in]  ULONG32 cMethod,  
    [out] ULONG32* pcMethod,  
    [out, size_is (cMethod),  
        length_is (*pcMethod)] ISymUnmanagedMethod* pRetVal[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `document`  
 から指定されたドキュメント。  
  
 `line`  
 から指定したドキュメントの行。  
  
 `column`  
 から指定されたドキュメントの列。  
  
 `cMethod`  
 [in] `pRetVal` 配列のサイズ。  
  
 `pcMethod`  
 入出力配列で返された要素の数を受け取る変数へのポインター `pRetVal` 。  
  
 `pRetVal`  
 入出力ポインターの配列。各ポインターは、ブレークポイントを含むメソッドを表す[ISymUnmanagedMethod](isymunmanagedmethod-interface.md)オブジェクトを指します。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedReader インターフェイス](isymunmanagedreader-interface.md)
