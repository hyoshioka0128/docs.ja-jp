---
title: ISymUnmanagedWriter4 インターフェイス
ms.date: 03/30/2017
ms.assetid: 4af5e8c0-987d-405e-b934-8b9e70fcae6e
ms.openlocfilehash: 21d6520aae1367368973da1692f6bca3aeb2c129
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84493657"
---
# <a name="isymunmanagedwriter4-interface"></a>ISymUnmanagedWriter4 インターフェイス
ISymUnmanagedWriter4 インターフェイス。  
  
## <a name="syntax"></a>構文  
  
```idl  
[object,uuid(BC7E3F53-F458-4C23-9DBD-A189E6E96594),pointer_default(unique)]interface ISymUnmanagedWriter4 : ISymUnmanagedWriter3  
```  
  
## <a name="methods"></a>メソッド  
 このインターフェイスには、次のメソッドが含まれています。  
  
|Method|説明|  
|------------|-----------------|  
|[GetDebugInfoWithPadding メソッド](isymunmanagedwriter4-getdebuginfowithpadding-method.md)|関数は[GetDebugInfo メソッド](isymunmanagedwriter-getdebuginfo-method.md)と同じですが、文字列データを固定サイズにするために、終端の null 文字の後にパス文字列がゼロで埋め込まれる点が異なり `MAX_PATH` ます。 埋め込みは、パス文字列の長さがより小さい場合にのみ指定 `MAX_PATH` します。<br /><br /> これにより、PE ファイルを区別するツールを簡単に記述できるようになります。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedWriter3 インターフェイス](isymunmanagedwriter3-interface.md)
