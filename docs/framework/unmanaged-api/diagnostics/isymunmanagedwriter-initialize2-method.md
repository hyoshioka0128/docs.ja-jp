---
title: ISymUnmanagedWriter::Initialize2 メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.Initialize2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::Initialize2
helpviewer_keywords:
- ISymUnmanagedWriter::Initialize2 method [.NET Framework debugging]
- Initialize2 method [.NET Framework debugging]
ms.assetid: 93de56b6-4ae8-4cca-acdc-25a434623509
topic_type:
- apiref
ms.openlocfilehash: 869d7d36ac24bfeee5b2361dd569945ad77eaf7f
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610068"
---
# <a name="isymunmanagedwriterinitialize2-method"></a>ISymUnmanagedWriter::Initialize2 メソッド
このライターが関連付けられるメタデータエミッタインターフェイスを設定し、デバッグシンボルの書き込み先となる出力ファイル名を設定します。 この方法では、プログラムデータベース (PDB) ファイルの最終的な場所を設定することもできます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Initialize2(  
    [in] IUnknown     *emitter,  
    [in] const WCHAR  *tempfilename,  
    [in] IStream      *pIStream,  
    [in] BOOL         fFullBuild,  
    [in] const WCHAR  *finalfilename);  
```  
  
## <a name="parameters"></a>パラメーター  
 `emitter`  
 からメタデータエミッタインターフェイスへのポインター。  
  
 `tempfilename`  
 から`WCHAR`デバッグシンボルが書き込まれるファイル名を格納しているへのポインター。 ファイル名を使用しないライターに対してファイル名を指定した場合、このパラメーターは無視されます。  
  
 `pIStream`  
 から指定されている場合、シンボルライターは、 <xref:System.Runtime.InteropServices.ComTypes.IStream> パラメーターで指定されたファイルではなく、指定されたにシンボルを出力し `filename` ます。 `pIStream` パラメーターは省略可能です。  
  
 `fFullBuild`  
 [入力] `true`完全な再構築の場合は、`false`インクリメンタルコンパイルの場合は。  
  
 `finalfilename`  
 から`WCHAR`PDB ファイルの最終的な場所へのパス文字列であるへのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
- [Initialize メソッド](isymunmanagedwriter-initialize-method.md)
