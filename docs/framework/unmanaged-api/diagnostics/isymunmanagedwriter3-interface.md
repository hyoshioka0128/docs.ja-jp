---
title: ISymUnmanagedWriter3 インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter3
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter3
helpviewer_keywords:
- ISymUnmanagedWriter3 interface [.NET Framework debugging]
ms.assetid: a034c21e-e371-4360-b470-29e88288948f
topic_type:
- apiref
ms.openlocfilehash: 006045ce101884119f676e4f6324815eb21a10a4
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614657"
---
# <a name="isymunmanagedwriter3-interface"></a>ISymUnmanagedWriter3 インターフェイス
シンボルライターを表し、ドキュメント、シーケンスポイント、構文スコープ、および変数を定義するメソッドを提供します。 このインターフェイスは、 [ISymUnmanagedWriter](isymunmanagedwriter-interface.md)インターフェイスを拡張します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Commit メソッド](isymunmanagedwriter3-commit-method.md)|これまでに書き込まれた変更をストリームにコミットします。|  
|[OpenMethod2 メソッド](isymunmanagedwriter3-openmethod2-method.md)|メソッドを開き、イメージ内の実際のセクションオフセットを提供します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
- [ISymUnmanagedWriter2 インターフェイス](isymunmanagedwriter2-interface.md)
