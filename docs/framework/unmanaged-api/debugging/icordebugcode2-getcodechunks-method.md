---
title: ICorDebugCode2::GetCodeChunks メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugCode2.GetCodeChunks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode2::GetCodeChunks
helpviewer_keywords:
- GetCodeChunks method [.NET Framework debugging]
- ICorDebugCode2::GetCodeChunks method [.NET Framework debugging]
ms.assetid: 210a2f02-2678-4555-bc4a-78a0408764c8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1bdaf6391ca5c19f073708d6258ad5775bec9824
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700725"
---
# <a name="icordebugcode2getcodechunks-method"></a>ICorDebugCode2::GetCodeChunks メソッド

このコード オブジェクトを構成しているコード チャンクを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCodeChunks (
    [in]  ULONG32     cbufSize,
    [out] ULONG32     *pcnumChunks,
    [out, size_is(cbufSize), length_is(*pcnumChunks)]
        CodeChunkInfo chunks[]
);
```

## <a name="parameters"></a>パラメーター

 `cbufSize`  
 から@No__t-0 配列のサイズ。

 `pcnumChunks`  
 入出力@No__t-0 配列で返されたチャンクの数。

 `chunks`  
 入出力"CodeChunkInfo" 構造体の配列。それぞれが1つのコードチャンクを表します。 @No__t-0 の値が0の場合、このパラメーターには null を指定できます。

## <a name="remarks"></a>コメント

 コードチャンクは重複しません。コードチャンクは、「[コード:: GetCode](icordebugcode-getcode-method.md)」によって連結された順序に従います。 .NET Framework バージョン2.0 の Microsoft 中間言語 (MSIL) コードオブジェクトは、1つのコードチャンクを構成します。

## <a name="requirements"></a>要件

 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。

 **ヘッダー:** CorDebug .idl、CorDebug. h

 **ライブラリ**CorGuids .lib

 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
 
