---
title: ISymUnmanagedWriter::SetMethodSourceRange メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.SetMethodSourceRange
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::SetMethodSourceRange
helpviewer_keywords:
- SetMethodSourceRange method [.NET Framework debugging]
- ISymUnmanagedWriter::SetMethodSourceRange method [.NET Framework debugging]
ms.assetid: c698b86e-ace7-4b21-9549-f52d6a034959
topic_type:
- apiref
ms.openlocfilehash: 4ba3f31ae6d6b67d7beaa2f709bf6174b721136d
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609522"
---
# <a name="isymunmanagedwritersetmethodsourcerange-method"></a>ISymUnmanagedWriter::SetMethodSourceRange メソッド
ソース ファイル内にメソッドの実際の先頭と末尾を指定します。 メソッドの範囲を、メソッド内に存在するシーケンスポイントとは別に指定するには、このメソッドを使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetMethodSourceRange(  
    [in] ISymUnmanagedDocumentWriter  *startDoc,  
    [in] ULONG32                      startLine,  
    [in] ULONG32                      startColumn,  
    [in] ISymUnmanagedDocumentWriter  *endDoc,  
    [in] ULONG32                      endLine,  
    [in] ULONG32                      endColumn);  
```  
  
## <a name="parameters"></a>パラメーター  
 `startDoc`  
 から開始位置を格納しているドキュメントへのポインター。  
  
 `startLine`  
 から開始行番号。  
  
 `startColumn`  
 から開始列。  
  
 `endDoc`  
 から終了位置を含むドキュメントへのポインター。  
  
 `endLine`  
 から終了行番号。  
  
 `endColumn`  
 から終了列番号。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
