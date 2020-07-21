---
title: ISymUnmanagedMethod::GetRanges メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetRanges
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetRanges
helpviewer_keywords:
- ISymUnmanagedMethod::GetRanges method [.NET Framework debugging]
- GetRanges method [.NET Framework debugging]
ms.assetid: a85283d8-379c-417a-9736-ddeeef9bcf50
topic_type:
- apiref
ms.openlocfilehash: cd5d1f2d59d3e55ba454f23d2e5dd4b1316c0df4
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615177"
---
# <a name="isymunmanagedmethodgetranges-method"></a>ISymUnmanagedMethod::GetRanges メソッド
ドキュメント内の位置が指定されている場合、は、位置がこのメソッド内でカバーする Microsoft 中間言語 (MSIL) の範囲に対応する開始オフセットと終了オフセットのペアの配列を返します。 配列は整数の配列であり、[開始、終了、開始、終了] の形式です。 範囲ペアの数は、配列の長さを2で除算した値です。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetRanges(  
    [in]  ISymUnmanagedDocument* document,  
    [in]  ULONG32                line,  
    [in]  ULONG32                column,  
    [in]  ULONG32                cRanges,  
    [out] ULONG32                *pcRanges,  
    [out, size_is(cRanges),  
        length_is(*pcRanges)] ULONG32 ranges[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `document`  
 からオフセットが要求されるドキュメント。  
  
 `line`  
 から範囲に対応するドキュメント行。  
  
 `column`  
 から範囲に対応するドキュメント列。  
  
 `cRanges`  
 [in] `ranges` 配列のサイズ。  
  
 `pcRanges`  
 入出力`ULONG32`範囲を格納するために必要なバッファーのサイズを受け取るへのポインター。  
  
 `ranges`  
 入出力範囲を受け取るバッファーへのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedMethod インターフェイス](isymunmanagedmethod-interface.md)
