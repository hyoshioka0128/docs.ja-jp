---
title: ISymUnmanagedReader2::GetSymAttributePreRemap メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader2.GetSymAttributePreRemap
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader2::GetSymAttributePreRemap
helpviewer_keywords:
- GetSymAttributePreRemap method [.NET Framework debugging]
- ISymUnmanagedReader2::GetSymAttributePreRemap method [.NET Framework debugging]
ms.assetid: 7580d546-a709-40c5-ad02-aa70d774fd0b
topic_type:
- apiref
ms.openlocfilehash: e6248aba1c41b2815f2806942d419da869ed94b4
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614917"
---
# <a name="isymunmanagedreader2getsymattributepreremap-method"></a>ISymUnmanagedReader2::GetSymAttributePreRemap メソッド
名前に基づいてカスタム属性を取得します。 メタデータのカスタム属性とは異なり、これらの属性はシンボルストアに保持されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetSymAttributePreRemap(  
    [in]  mdToken  parent,  
    [in]  WCHAR    *name,  
    [in]  ULONG32  cBuffer,  
    [out] ULONG32  *pcBuffer,  
    [out, size_is(cBuffer),  
        length_is(*pcBuffer)] BYTE buffer[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `parent`  
 から親のメタデータトークン。  
  
 `name`  
 から名前を格納し `WCHAR` ているへのポインター。  
  
 `cBuffer`  
 から`ULONG32`配列のサイズを示す `buffer` 。  
  
 `pcBuffer`  
 入出力`ULONG32`属性バイトを格納するために必要なバッファーのサイズを受け取るへのポインター。  
  
 `buffer`  
 入出力属性バイトを受け取るバッファーへのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedReader2 インターフェイス](isymunmanagedreader2-interface.md)
