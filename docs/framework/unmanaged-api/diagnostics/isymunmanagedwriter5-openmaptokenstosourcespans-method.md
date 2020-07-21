---
title: ISymUnmanagedWriter5::OpenMapTokensToSourceSpans メソッド
ms.date: 03/30/2017
ms.assetid: 93ad2517-b0dc-464c-8688-a58a30eda18d
ms.openlocfilehash: 82b46ea315009b65254735d44e355154b83b22e2
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609496"
---
# <a name="isymunmanagedwriter5openmaptokenstosourcespans-method"></a>ISymUnmanagedWriter5::OpenMapTokensToSourceSpans メソッド
特別なカスタムデータセクションを開き、トークンからソースまでの範囲マッピング情報をに出力します。 メソッドが既に開いている場合や、その逆の場合にこのセクションを開くと、エラーになります。  
  
## <a name="syntax"></a>構文  
  
```idl  
HRESULT OpenMapTokensToSourceSpans();  
```  
  
## <a name="return-value"></a>戻り値  
 `HRESULT` を返します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter5 インターフェイス](isymunmanagedwriter5-interface.md)
