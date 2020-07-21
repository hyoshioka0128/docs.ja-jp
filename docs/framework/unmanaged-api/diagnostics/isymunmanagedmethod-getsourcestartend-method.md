---
title: ISymUnmanagedMethod::GetSourceStartEnd メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetSourceStartEnd
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetSourceStartEnd
helpviewer_keywords:
- GetSourceStartEnd method [.NET Framework debugging]
- ISymUnmanagedMethod::GetSourceStartEnd method [.NET Framework debugging]
ms.assetid: 2a420900-01f1-4461-8777-3a34a6dc1426
topic_type:
- apiref
ms.openlocfilehash: 25e797fdf563a01ab727f16e7173eec2552eeb27
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614423"
---
# <a name="isymunmanagedmethodgetsourcestartend-method"></a>ISymUnmanagedMethod::GetSourceStartEnd メソッド
このメソッドのソースのドキュメントの開始位置と終了位置を取得します。 最初の配列の位置は start で、2番目の配列の位置は末尾です。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetSourceStartEnd(  
    [in]  ISymUnmanagedDocument  *docs[2],  
    [in]  ULONG32                lines[2],  
    [in]  ULONG32                columns[2],  
    [out] BOOL                   *pRetVal);  
```  
  
## <a name="parameters"></a>パラメーター  
 `docs`  
 から開始と終了のソースドキュメント。  
  
 `lines`  
 から対応するソースドキュメントの開始行と終了行。  
  
 `columns`  
 から対応するソースドキュメント内の開始列と終了列。  
  
 `pRetVal`  
 [出力] `true`位置が定義されている場合は。それ以外の場合は `false` 。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedMethod インターフェイス](isymunmanagedmethod-interface.md)
