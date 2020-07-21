---
title: ISymUnmanagedWriter::RemapToken メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.RemapToken
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::RemapToken
helpviewer_keywords:
- ISymUnmanagedWriter::RemapToken method [.NET Framework debugging]
- RemapToken method [.NET Framework debugging]
ms.assetid: bca92682-ee1e-467f-8fb0-d8d4617f82fe
topic_type:
- apiref
ms.openlocfilehash: 53cc908e0dc8cc5cc980ec365ccac0df4e620cac
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609769"
---
# <a name="isymunmanagedwriterremaptoken-method"></a>ISymUnmanagedWriter::RemapToken メソッド
メタデータが生成されたときにメタデータトークンが再マップされたことをシンボルライターに通知します。 シンボルライターがシンボルストア内に古いトークンを格納している場合は、格納されているトークンを新しい値で更新するか、読み取りフェーズ中に対応するシンボルリーダーがマップを再マップするようにマップを保存する必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RemapToken(  
    [in] mdToken  oldToken,  
    [in] mdToken  newToken);  
```  
  
## <a name="parameters"></a>パラメーター  
 `oldToken`  
 から再マップされたメタデータトークン。  
  
 `newToken`  
 からが再マップされた新しいメタデータトークン `oldToken` 。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
