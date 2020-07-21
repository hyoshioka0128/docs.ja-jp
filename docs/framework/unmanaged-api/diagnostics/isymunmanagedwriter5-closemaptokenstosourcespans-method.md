---
title: ISymUnmanagedWriter5::CloseMapTokensToSourceSpans メソッド
ms.date: 03/30/2017
ms.assetid: f8a0c0a2-a11d-436c-aa85-bc110215cfd6
ms.openlocfilehash: 053727604c795bf43a9b1658d5841fe85f53090a
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614631"
---
# <a name="isymunmanagedwriter5closemaptokenstosourcespans-method"></a>ISymUnmanagedWriter5::CloseMapTokensToSourceSpans メソッド
トークンとソースの間のマッピング情報については、特別なカスタムデータセクションを閉じます。 閉じた後は、マッピング情報を追加することはできません。  
  
## <a name="syntax"></a>構文  
  
```idl  
HRESULT CloseMapTokensToSourceSpans();  
```  
  
## <a name="return-value"></a>戻り値  
 `HRESULT` を返します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter5 インターフェイス](isymunmanagedwriter5-interface.md)
