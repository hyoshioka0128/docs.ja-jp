---
title: ISymUnmanagedWriter4::GetDebugInfoWithPadding メソッド
ms.date: 03/30/2017
ms.assetid: 881e20ca-8131-4bd0-ba41-c2d6391b0fe2
ms.openlocfilehash: cfc6c22558cee780823c8cca0c36b883147e9496
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614644"
---
# <a name="isymunmanagedwriter4getdebuginfowithpadding-method"></a>ISymUnmanagedWriter4::GetDebugInfoWithPadding メソッド
関数は[GetDebugInfo メソッド](isymunmanagedwriter-getdebuginfo-method.md)と同じですが、文字列データを固定サイズにするために、終端の null 文字の後にパス文字列がゼロで埋め込まれる点が異なり `MAX_PATH` ます。 埋め込みは、パス文字列の長さがより小さい場合にのみ指定 `MAX_PATH` します。  
  
 これにより、PE ファイルを区別するツールを簡単に記述できるようになります。  
  
## <a name="syntax"></a>構文  
  
```idl  
HRESULT GetDebugInfoWithPadding(    [in, out] IMAGE_DEBUG_DIRECTORY *pIDD,    [in] DWORD cData,    [out] DWORD *pcData,    [out, size_is(cData), length_is(*pcData)] BYTE data[]);  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`pIDD`||  
|`cData`||  
|`pcData`||  
|`data`||  
  
## <a name="return-value"></a>戻り値  
 `HRESULT` を返します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter4 インターフェイス](isymunmanagedwriter4-interface.md)
