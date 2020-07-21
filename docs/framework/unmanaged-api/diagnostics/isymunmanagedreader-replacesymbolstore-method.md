---
title: ISymUnmanagedReader::ReplaceSymbolStore メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.ReplaceSymbolStore
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::ReplaceSymbolStore
helpviewer_keywords:
- ReplaceSymbolStore method [.NET Framework debugging]
- ISymUnmanagedReader::ReplaceSymbolStore method [.NET Framework debugging]
ms.assetid: 43257761-8cb1-4eaf-8fb5-1f3980cb66cd
topic_type:
- apiref
ms.openlocfilehash: db2137146ded5200e05bbf88e23ae599f3eb7dec
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615450"
---
# <a name="isymunmanagedreaderreplacesymbolstore-method"></a>ISymUnmanagedReader::ReplaceSymbolStore メソッド
既存のシンボル ストアをデルタ シンボル ストアで置き換えます。 このメソッドは、指定されたデルタが更新ではなく完全な置換として機能する点を除いて、"更新プログラム"[ストア](isymunmanagedreader-updatesymbolstore-method.md)メソッドに似ています。  
  
> [!NOTE]
> またはパラメーターのいずれか1つだけを指定する必要があります。両方を指定すること `filename` はでき `pIStream` ません。 を `filename` 指定した場合、シンボルストアはそのファイル内のシンボルで更新されます。 を指定した場合、 `pIStream` ストアはからのデータで更新され <xref:System.Runtime.InteropServices.ComTypes.IStream> ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ReplaceSymbolStore (  
    [in] const WCHAR *filename,  
    [in] IStream *pIStream);  
```  
  
## <a name="parameters"></a>パラメーター  
 `filename`  
 からシンボルストアを格納しているファイルの名前。  
  
 `pIStream`  
 からパラメーターの代わりに使用されるファイルストリーム `filename` 。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedReader インターフェイス](isymunmanagedreader-interface.md)
