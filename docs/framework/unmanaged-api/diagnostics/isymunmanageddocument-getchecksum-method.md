---
title: ISymUnmanagedDocument::GetCheckSum メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument.GetCheckSum
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument::GetCheckSum
helpviewer_keywords:
- ISymUnmanagedDocument::GetCheckSum method [.NET Framework debugging]
- GetCheckSum method [.NET Framework debugging]
ms.assetid: 9bc881b3-e2ce-48a7-ad69-17eaaa304120
topic_type:
- apiref
ms.openlocfilehash: 543bd208e5492460435663c32f276472a763f613
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441098"
---
# <a name="isymunmanageddocumentgetchecksum-method"></a>ISymUnmanagedDocument::GetCheckSum メソッド
チェックサムを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCheckSum(  
    [in]  ULONG32  cData,  
    [out] ULONG32  *pcData,  
    [out, size_is(cData), length_is(*pcData)] BYTE data[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cData`  
 からパラメーターによって指定されたバッファーの長さ `data`  
  
 `pcData`  
 入出力チェックサムのサイズと長さ (バイト単位)。  
  
 `data`  
 入出力チェックサムを受け取るバッファー。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、エラーコード。  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedDocument インターフェイス](isymunmanageddocument-interface.md)
