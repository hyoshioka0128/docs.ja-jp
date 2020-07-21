---
title: ISymENCUnmanagedMethod::GetDocumentsForMethod メソッド
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetDocumentsForMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetDocumentsForMethod
helpviewer_keywords:
- GetDocumentsForMethod method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetDocumentsForMethod method [.NET Framework debugging]
ms.assetid: bd6ccde5-d578-48d8-abed-b474fbd48d13
topic_type:
- apiref
ms.openlocfilehash: 89be772ee3d8a6fc5acb74d5ebe6d3c691764f89
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441956"
---
# <a name="isymencunmanagedmethodgetdocumentsformethod-method"></a>ISymENCUnmanagedMethod::GetDocumentsForMethod メソッド
このメソッドに行が含まれているドキュメントを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetDocumentsForMethod(  
    [in]  ULONG32  cDocs,  
    [out] ULONG32  *pcDocs,
    [in, size_is(cDocs)] ISymUnmanagedDocument* documents[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cDocs`  
 からが指すバッファーの長さ `pcDocs` 。  
  
 `pcDocs`  
 入出力`ULONG32`ドキュメントを格納するために必要なバッファーのサイズ (文字数) を受け取るへのポインター。  
  
 `documents`  
 からドキュメントを格納しているバッファー。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、エラーコード。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymENCUnmanagedMethod インターフェイス](isymencunmanagedmethod-interface.md)
