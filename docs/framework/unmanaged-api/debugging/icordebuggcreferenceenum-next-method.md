---
title: ICorDebugGCReferenceEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugGCReferenceEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugGCReferenceEnum::Next
helpviewer_keywords:
- Next method, ICorDebugGCReferenceEnum interface [.NET Framework debugging]
- ICorDebugGCReferenceEnum::Next method [.NET Framework debugging]
ms.assetid: 91b1345c-a94f-4ef8-9696-3823d06c6d05
topic_type:
- apiref
ms.openlocfilehash: 1cf6f9c5fe8777f3333e449a804a3c3a0a64ff19
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213089"
---
# <a name="icordebuggcreferenceenumnext-method"></a>ICorDebugGCReferenceEnum::Next メソッド
ガベージコレクトされるオブジェクトに関する情報を格納している、指定した数の[COR_GC_REFERENCE](cor-gc-reference-structure.md)インスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next(  
    [in] ULONG celt,    [out, size_is(celt), length_is(*pceltFetched)] COR_GC_REFERENCE roots[],
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 celt  
 から取得するルートの数。  
  
 ca  
 入出力ポインターの配列。各ポインターは、ガベージコレクトされるオブジェクトのルートを表す[COR_GC_REFERENCE](cor-gc-reference-structure.md)オブジェクトを指します。  
  
 pceltFetched  
 入出力実際にで返される[COR_GC_REFERENCE](cor-gc-reference-structure.md)オブジェクトの数へのポインター `roots` 。 `celt` が 1 の場合、この値は`null` になることがあります。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugGCReferenceEnum インターフェイス](icordebuggcreferenceenum-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
