---
title: ISymUnmanagedWriter::Abort メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.Abort
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::Abort
helpviewer_keywords:
- ISymUnmanagedWriter::Abort method [.NET Framework debugging]
- Abort method, ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: 416b220f-38d4-48e0-bb49-d2faa7366702
topic_type:
- apiref
ms.openlocfilehash: 09f39d3b6486e2ec3c04c5d1858a85ce56895527
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610159"
---
# <a name="isymunmanagedwriterabort-method"></a>ISymUnmanagedWriter::Abort メソッド
シンボルストアにシンボルをコミットせずにシンボルライターを閉じます。 この呼び出しの後、シンボルライターは、さらに更新するために無効になります。 シンボルをコミットし、シンボルライターを閉じるには、代わりに[ISymUnmanagedWriter:: close](isymunmanagedwriter-close-method.md)メソッドを使用します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Abort();  
```  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
