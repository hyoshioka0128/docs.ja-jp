---
title: ISymUnmanagedReaderSymbolSearchInfo インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReaderSymbolSearchInfo
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReaderSymbolSearchInfo
helpviewer_keywords:
- ISymUnmanagedReaderSymbolSearchInfo interface [.NET Framework debugging]
ms.assetid: fde7e21d-1169-4bed-a34d-792e69652bf9
topic_type:
- apiref
ms.openlocfilehash: 3f6cea68a4379f8769ccbdbc6911cc5c425d3369
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614878"
---
# <a name="isymunmanagedreadersymbolsearchinfo-interface"></a>ISymUnmanagedReaderSymbolSearchInfo インターフェイス
シンボル検索情報を取得するメソッドを提供します。 このインターフェイスを取得するには `QueryInterface` 、 [ISymUnmanagedReader](isymunmanagedreader-interface.md)インターフェイスを実装するオブジェクトに対してを呼び出します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetSymbolSearchInfo メソッド](isymunmanagedreadersymbolsearchinfo-getsymbolsearchinfo-method.md)|シンボルの検索情報を取得します。|  
|[GetSymbolSearchInfoCount メソッド](isymunmanagedreadersymbolsearchinfo-getsymbolsearchinfocount-method.md)|シンボル検索情報の数を取得します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
