---
title: SYMLINEDELTA 構造体
ms.date: 03/30/2017
api_name:
- SYMLINEDELTA
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- SYMLINEDELTA
helpviewer_keywords:
- SYMLINEDELTA structure [.NET Framework debugging]
ms.assetid: 9634e995-d46d-4397-ab66-cc5781d11e4e
topic_type:
- apiref
ms.openlocfilehash: fb3b89d25b4c2e23c3980b167db4279246c4d27b
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609301"
---
# <a name="symlinedelta-structure"></a>SYMLINEDELTA 構造体
編集の結果として移動されたメソッドについて、シンボルハンドラーに情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _SYMLINEDELTA  
    {  
        mdMethodDef  mdMethod;  
        INT32        delta;  
    } SYMLINEDELTA;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`mdMethod`|メソッドのメタデータトークン。|  
|`delta`|メソッドが移動された行の数。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断構造体](diagnostics-symbol-store-structures.md)
