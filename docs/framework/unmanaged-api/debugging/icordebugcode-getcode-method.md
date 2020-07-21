---
title: ICorDebugCode::GetCode メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetCode
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetCode
helpviewer_keywords:
- ICorDebugCode::GetCode method [.NET Framework debugging]
- GetCode method, ICorDebugCode interface [.NET Framework debugging]
ms.assetid: 7137e3d1-1dad-48d8-8c37-16ac816534d3
topic_type:
- apiref
ms.openlocfilehash: 59a497d203d241bbc6e0f884007d4a401c112073
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893654"
---
# <a name="icordebugcodegetcode-method"></a>ICorDebugCode::GetCode メソッド
指定した関数のすべてのコードを取得し、逆アセンブリ用に書式設定します。 このメソッドは .NET Framework バージョン2.0 では非推奨とされました。 代わりに[ICorDebugCode2:: GetCodeChunks](icordebugcode2-getcodechunks-method.md)を使用してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCode (  
    [in] ULONG32     startOffset,
    [in] ULONG32     endOffset,  
    [in] ULONG32     cBufferAlloc,  
    [out, size_is(cBufferAlloc),  
        length_is(*pcBufferSize)] BYTE buffer[],  
    [out] ULONG32    *pcBufferSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `startOffset`  
 から関数の開始位置のオフセット。  
  
 `endOffset`  
 から関数の終了位置のオフセット。  
  
 `cBufferAlloc`  
 からコードが返される`buffer`配列のサイズ。  
  
 `buffer`  
 入出力コードが返される配列。  
  
 `pcBufferSize`  
 入出力返されたバイト数。  
  
## <a name="remarks"></a>解説  
 関数のコードが複数のチャンクに分割されている場合は、ネイティブオフセットが増加する順序で連結されます。 命令の境界はチェックされません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** 1.1、1.0  
  
## <a name="see-also"></a>関連項目

- [GetCodeChunks メソッド](icordebugcode2-getcodechunks-method.md)
