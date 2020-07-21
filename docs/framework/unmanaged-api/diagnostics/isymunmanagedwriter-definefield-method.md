---
title: ISymUnmanagedWriter::DefineField メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineField
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineField
helpviewer_keywords:
- ISymUnmanagedWriter::DefineField method [.NET Framework debugging]
- DefineField method, ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: c6a1f797-dbf4-40f5-ab99-d9b4bfb26148
topic_type:
- apiref
ms.openlocfilehash: aba551a1973a41a909869316cda07e8d655e9882
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614839"
---
# <a name="isymunmanagedwriterdefinefield-method"></a>ISymUnmanagedWriter::DefineField メソッド
メソッド内にない単一の変数を定義します。 このメソッドは、クラス、ビットフィールドなどの特定のフィールドに対して使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineField(  
    [in] mdTypeDef    parent,  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] ULONG32      cSig,  
    [in, size_is(cSig)] unsigned char signature[],  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3);  
```  
  
## <a name="parameters"></a>パラメーター  
 `parent`  
 からメタデータ型またはメソッドトークン。  
  
 `name`  
 からフィールド名。  
  
 `attributes`  
 からフィールド属性。  
  
 `cSig`  
 から`ULONG32`フィールドシグネチャを格納するために必要なバッファーのサイズ (文字数) を表す。  
  
 `signature`  
 からフィールドシグネチャの配列。  
  
 `addrKind`  
 からアドレスの種類。  
  
 `addr1`  
 からフィールド指定の最初のアドレス。  
  
 `addr2`  
 からフィールド指定の2番目のアドレス。  
  
 `addr3`  
 からフィールド指定の3番目のアドレス。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
