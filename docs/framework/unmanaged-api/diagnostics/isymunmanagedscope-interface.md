---
title: ISymUnmanagedScope インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope
helpviewer_keywords:
- ISymUnmanagedScope interface [.NET Framework debugging]
ms.assetid: 3db7a220-cfe9-4810-8ca8-a094bb8e0f5b
topic_type:
- apiref
ms.openlocfilehash: 1ee406c97fa4ccb7f87098cba2925568d8ce069f
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615346"
---
# <a name="isymunmanagedscope-interface"></a>ISymUnmanagedScope インターフェイス
メソッド内の構文のスコープを表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetChildren メソッド](isymunmanagedscope-getchildren-method.md)|このスコープの子を取得します。|  
|[GetEndOffset メソッド](isymunmanagedscope-getendoffset-method.md)|このスコープの終了オフセットを取得します。|  
|[GetLocalCount メソッド](isymunmanagedscope-getlocalcount-method.md)|このスコープ内で定義されているローカル変数の数を取得します。|  
|[GetLocals メソッド](isymunmanagedscope-getlocals-method.md)|このスコープ内で定義されているローカル変数を取得します。|  
|[GetMethod メソッド](isymunmanagedscope-getmethod-method.md)|このスコープを格納しているメソッドを取得します。|  
|[GetNamespaces メソッド](isymunmanagedscope-getnamespaces-method.md)|このスコープ内で使用されている名前空間を取得します。|  
|[GetParent メソッド](isymunmanagedscope-getparent-method.md)|このスコープの親スコープを取得します。|  
|[GetStartOffSet メソッド](isymunmanagedscope-getstartoffset-method.md)|このスコープの開始オフセットを取得します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedScope2 インターフェイス](isymunmanagedscope2-interface.md)
