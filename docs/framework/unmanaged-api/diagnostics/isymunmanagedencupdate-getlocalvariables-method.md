---
title: ISymUnmanagedENCUpdate::GetLocalVariables メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedENCUpdate.GetLocalVariables
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedENCUpdate::GetLocalVariables
helpviewer_keywords:
- ISymUnmanagedENCUpdate::GetLocalVariables method [.NET Framework debugging]
- GetLocalVariables method [.NET Framework debugging]
ms.assetid: 5c8840be-ffea-447f-9c8d-178f1eaf8d06
topic_type:
- apiref
ms.openlocfilehash: 5e5bf097a4b1e366fff807595b22c4696a91cf43
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614553"
---
# <a name="isymunmanagedencupdategetlocalvariables-method"></a>ISymUnmanagedENCUpdate::GetLocalVariables メソッド
ローカル変数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetLocalVariables(  
    [in]  mdMethodDef  mdMethodToken,  
    [in]  ULONG        cLocals,  
    [out, size_is(cLocals), length_is(*pceltFetched)]  
        ISymUnmanagedVariable *rgLocals[],  
    [out] ULONG        *pceltFetched);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mdMethodToken`  
 からメソッドのメタデータトークン。  
  
 `cLocals`  
 から`ULONG`パラメーターのサイズを示す `rgLocals` 。  
  
 `rgLocals`  
 入出力返される[ISymUnmanagedVariable](isymunmanagedvariable-interface.md)インスタンスの配列。  
  
 `pceltFetched`  
 入出力`ULONG` `rgLocals` ローカルを格納するために必要なバッファーのサイズを受け取るへのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedENCUpdate インターフェイス](isymunmanagedencupdate-interface.md)
