---
title: ISymENCUnmanagedMethod::GetLineFromOffset メソッド
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetLineFromOffset
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetLineFromOffset
helpviewer_keywords:
- GetLineFromOffset method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetLineFromOffset method [.NET Framework debugging]
ms.assetid: cc09bad2-fb34-4d13-a521-6ec7b1a1d915
topic_type:
- apiref
ms.openlocfilehash: d9a7b18e90a3038c1ffb634ccc7315143875c809
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441917"
---
# <a name="isymencunmanagedmethodgetlinefromoffset-method"></a>ISymENCUnmanagedMethod::GetLineFromOffset メソッド
オフセットに関連付けられている行情報を取得します。 オフセットパラメーター ( `dwOffset` ) がシーケンスポイントでない場合、このメソッドは、前のオフセットに関連付けられている行情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetLineFromOffset(  
     [in]  ULONG32   dwOffset,  
     [out] ULONG32*  pline,  
     [out] ULONG32*  pcolumn,  
     [out] ULONG32*  pendLine,  
     [out] ULONG32*  pendColumn,  
     [out] ULONG32*  pdwStartOffset);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwOffset`  
 から`ULONG32`オフセットを格納している。  
  
 `pline`  
 入出力行を受け取るへのポインター `ULONG32` 。  
  
 `pcolumn`  
 入出力列を受け取るへのポインター `ULONG32` 。  
  
 `pendLine`  
 入出力終了行を受け取るへのポインター `ULONG32` 。  
  
 `pendColumn`  
 入出力終了列を受け取るへのポインター `ULONG32` 。  
  
 `pdwStartOffset`  
 入出力`ULONG32`関連付けられたシーケンスポイントを受け取るへのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymENCUnmanagedMethod インターフェイス](isymencunmanagedmethod-interface.md)
