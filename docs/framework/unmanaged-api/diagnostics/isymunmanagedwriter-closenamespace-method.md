---
title: ISymUnmanagedWriter::CloseNamespace メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.CloseNamespace
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::CloseNamespace
helpviewer_keywords:
- ISymUnmanagedWriter::CloseNamespace method [.NET Framework debugging]
- CloseNamespace method [.NET Framework debugging]
ms.assetid: 7f74d9c5-1377-4958-b842-6306d611cbd5
topic_type:
- apiref
ms.openlocfilehash: 7a4ffc0c417ae839e5c97ffe6884bc3230a603b7
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610107"
---
# <a name="isymunmanagedwriterclosenamespace-method"></a>ISymUnmanagedWriter::CloseNamespace メソッド
最近開いた名前空間を閉じます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CloseNamespace();  
```  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
- [OpenNamespace メソッド](isymunmanagedwriter-opennamespace-method.md)
