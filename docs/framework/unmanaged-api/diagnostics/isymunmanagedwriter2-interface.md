---
title: ISymUnmanagedWriter2 インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter2
helpviewer_keywords:
- ISymUnmanagedWriter2 interface [.NET Framework debugging]
ms.assetid: 8e78faa4-cf43-44fb-a91d-94d6df692a25
topic_type:
- apiref
ms.openlocfilehash: 1fe6055d930c6d30e947d6bc774d0520a9e175ae
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614683"
---
# <a name="isymunmanagedwriter2-interface"></a>ISymUnmanagedWriter2 インターフェイス
シンボルライターを表し、ドキュメント、シーケンスポイント、構文スコープ、および変数を定義するメソッドを提供します。 このインターフェイスは、 [ISymUnmanagedWriter](isymunmanagedwriter-interface.md)インターフェイスを拡張します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[DefineConstant2 メソッド](isymunmanagedwriter2-defineconstant2-method.md)|定数値の名前を定義します。|  
|[DefineGlobalVariable2 メソッド](isymunmanagedwriter2-defineglobalvariable2-method.md)|グローバル変数を 1 つ定義します。|  
|[DefineLocalVariable2 メソッド](isymunmanagedwriter2-definelocalvariable2-method.md)|現在の構文のスコープの変数を 1 つ定義します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
- [ISymUnmanagedWriter3 インターフェイス](isymunmanagedwriter3-interface.md)
