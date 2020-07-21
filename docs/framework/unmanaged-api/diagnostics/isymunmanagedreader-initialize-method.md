---
title: ISymUnmanagedReader::Initialize メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.Initialize
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::Initialize
helpviewer_keywords:
- ISymUnmanagedReader::Initialize method [.NET Framework debugging]
- Initialize method, ISymUnmanagedReader interface [.NET Framework debugging]
ms.assetid: 8f0dd2fe-7df7-464e-91f4-5518c586bb5f
topic_type:
- apiref
ms.openlocfilehash: 07d2de5d12fd769cb5cce243d9e721bb6fc185a7
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615476"
---
# <a name="isymunmanagedreaderinitialize-method"></a>ISymUnmanagedReader::Initialize メソッド
このリーダーが関連付けられるメタデータインポーターインターフェイスと、モジュールのファイル名を使用して、シンボルリーダーを初期化します。  
  
> [!NOTE]
> このメソッドを呼び出すことができるのは1回だけです。他のリーダーメソッドの前に呼び出す必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Initialize (  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *filename,  
    [in]  const WCHAR  *searchPath,  
    [in]  IStream      *pIStream);  
```  
  
## <a name="parameters"></a>パラメーター  
 `importer`  
 からこのリーダーが関連付けられるメタデータインポーターインターフェイス。  
  
 `filename`  
 からモジュールのファイル名。 代わりに、パラメーターを使用でき `pIStream` ます。  
  
 `searchPath`  
 から検索するパス。 このパラメーターは省略可能です。  
  
 `pIStream`  
 からファイルストリーム。 filename パラメーターの代わりに使用されます。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="remarks"></a>解説  
 またはパラメーターのいずれか1つだけを指定する必要があります。両方を指定すること `filename` はでき `pIStream` ません。 `searchPath` パラメーターは省略可能です。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedReader インターフェイス](isymunmanagedreader-interface.md)
