---
title: ISymUnmanagedDocument::GetLanguage メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.GetLanguage
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::GetLanguage
helpviewer_keywords:
- ISymUnmanagedDocument::GetLanguage method [.NET Framework debugging]
- GetLanguage method [.NET Framework debugging]
ms.assetid: c6639418-e9f2-4a99-8ce2-ec9876e0bc79
topic_type:
- apiref
ms.openlocfilehash: 084f3ae12d906f5e80fdb86e65b09d2371fd246b
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614592"
---
# <a name="isymunmanageddocumentgetlanguage-method"></a>ISymUnmanagedDocument::GetLanguage メソッド
このドキュメントの言語識別子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetLanguage(  
    [out, retval]  GUID*  pRetVal);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pRetVal`  
 入出力言語識別子を受け取る変数へのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK します。  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedDocument インターフェイス](isymunmanageddocument-interface.md)
