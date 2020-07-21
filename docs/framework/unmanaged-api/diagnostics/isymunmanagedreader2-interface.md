---
title: ISymUnmanagedReader2 インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader2
helpviewer_keywords:
- ISymUnmanagedReader2 interface [.NET Framework debugging]
ms.assetid: a01a881b-82a3-4b3e-a3a9-9dc305c2e5f7
topic_type:
- apiref
ms.openlocfilehash: d4c5ff46d37b1292059b18920abd8042c18bbf31
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615398"
---
# <a name="isymunmanagedreader2-interface"></a>ISymUnmanagedReader2 インターフェイス
シンボルストア内のドキュメント、メソッド、および変数へのアクセスを提供するシンボルリーダーを表します。 このインターフェイスは、 [ISymUnmanagedReader](isymunmanagedreader-interface.md)インターフェイスを拡張します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetMethodByVersionPreRemap メソッド](isymunmanagedreader2-getmethodbyversionpreremap-method.md)|メソッドトークンとエディットコンティニュバージョン番号を指定して、シンボルリーダーメソッドを取得します。|  
|[GetMethodsInDocument メソッド](isymunmanagedreader2-getmethodsindocument-method.md)|指定されたドキュメントに行情報が含まれるすべてのメソッドを取得します。|  
|[GetSymAttributePreRemap メソッド](isymunmanagedreader2-getsymattributepreremap-method.md)|名前に基づいてカスタム属性を取得します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedReader インターフェイス](isymunmanagedreader-interface.md)
