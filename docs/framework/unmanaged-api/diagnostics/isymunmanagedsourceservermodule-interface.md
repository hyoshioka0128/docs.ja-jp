---
title: ISymUnmanagedSourceServerModule インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedSourceServerModule
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedSourceServerModule
helpviewer_keywords:
- ISymUnmanagedSourceServerModule interface [.NET Framework debugging]
ms.assetid: a19b23bd-2061-476e-b67d-252f57404f8b
topic_type:
- apiref
ms.openlocfilehash: d90a55b53ba00540137e44fc190790c4710903e3
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610796"
---
# <a name="isymunmanagedsourceservermodule-interface"></a>ISymUnmanagedSourceServerModule インターフェイス
モジュールのソースサーバーデータを提供します。 このインターフェイスを取得するには `QueryInterface` 、 [ISymUnmanagedReader](isymunmanagedreader-interface.md)インターフェイスを実装するオブジェクトに対してを呼び出します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetSourceServerData メソッド](isymunmanagedsourceservermodule-getsourceserverdata-method.md)|モジュールのソースサーバーデータを返します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
