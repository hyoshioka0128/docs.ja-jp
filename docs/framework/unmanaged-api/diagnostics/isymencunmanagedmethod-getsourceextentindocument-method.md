---
title: ISymENCUnmanagedMethod::GetSourceExtentInDocument メソッド
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetSourceExtentInDocument
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetSourceExtentInDocument
helpviewer_keywords:
- GetSourceExtentInDocument method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetSourceExtentInDocument method [.NET Framework debugging]
ms.assetid: 9c5566ab-4ec7-4b61-9753-839bb90ae78c
topic_type:
- apiref
ms.openlocfilehash: 3ac8bb3a20ce82b734a572832a9cbb75fa2568c4
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441904"
---
# <a name="isymencunmanagedmethodgetsourceextentindocument-method"></a>ISymENCUnmanagedMethod::GetSourceExtentInDocument メソッド
特定のドキュメント内のメソッドの最小の開始行と最大の終了行を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetSourceExtentInDocument(  
    [in]  ISymUnmanagedDocument *document,  
    [out] ULONG32* pstartLine,  
    [out] ULONG32* pendLine);  
```  
  
## <a name="parameters"></a>パラメーター  
 `document`  
 からドキュメントへのポインター。  
  
 `pstartLine`  
 入出力開始行を受け取るへのポインター `ULONG32` 。  
  
 `pendLine`  
 入出力終了行を受け取るへのポインター `ULONG32` 。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymENCUnmanagedMethod インターフェイス](isymencunmanagedmethod-interface.md)
