---
title: ISymUnmanagedWriter::Initialize メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.Initialize
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::Initialize
helpviewer_keywords:
- ISymUnmanagedWriter::Initialize method [.NET Framework debugging]
- Initialize method, ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: e0ebd793-3764-4df0-8f12-0e95f60b9eae
topic_type:
- apiref
ms.openlocfilehash: 1553e616f60b4f05c06b6457d47454dfb4bc2eb7
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614774"
---
# <a name="isymunmanagedwriterinitialize-method"></a>ISymUnmanagedWriter::Initialize メソッド
このライターが関連付けられるメタデータエミッタインターフェイスを設定し、デバッグシンボルの書き込み先となる出力ファイル名を設定します。  
  
 このメソッドを呼び出すことができるのは1回だけです。他のライターメソッドの前に呼び出す必要があります。 一部のライターでは、ファイル名が必要になる場合があります。 ただし、ファイル名を使用しないライターに悪影響を及ぼすことなく、常にファイル名をこのメソッドに渡すことができます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Initialize(  
    [in] IUnknown     *emitter,  
    [in] const WCHAR  *filename,  
    [in] IStream      *pIStream,  
    [in] BOOL         fFullBuild);  
```  
  
## <a name="parameters"></a>パラメーター  
 `emitter`  
 からメタデータエミッタインターフェイスへのポインター。  
  
 `filename`  
 からデバッグシンボルが書き込まれるファイル名。 ファイル名を使用しないライターに対してファイル名を指定した場合、このパラメーターは無視されます。  
  
 `pIStream`  
 から指定した場合、シンボルライターは、パラメーターで指定されたファイルではなく、指定されたにシンボルを出力し <xref:System.Runtime.InteropServices.ComTypes.IStream> `filename` ます。 `pIStream` パラメーターは省略可能です。  
  
 `fFullBuild`  
 [入力] `true`完全な再構築の場合は、`false`インクリメンタルコンパイルの場合は。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
- [Initialize2 メソッド](isymunmanagedwriter-initialize2-method.md)
