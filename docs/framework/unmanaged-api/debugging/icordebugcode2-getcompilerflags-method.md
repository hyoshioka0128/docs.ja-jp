---
title: ICorDebugCode2::GetCompilerFlags メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugCode2.GetCompilerFlags
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode2::GetCompilerFlags
helpviewer_keywords:
- GetCompilerFlags method [.NET Framework debugging]
- ICorDebugCode2::GetCompilerFlags method [.NET Framework debugging]
ms.assetid: 532e9dfd-d114-4c75-b952-1accce102643
topic_type:
- apiref
ms.openlocfilehash: 734a05d96aed309541708d4e6f80ed61cab85637
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893493"
---
# <a name="icordebugcode2getcompilerflags-method"></a>ICorDebugCode2::GetCompilerFlags メソッド

このコード オブジェクトが Just-In-Time (JIT) コンパイルされたとき、またはネイティブ イメージ ジェネレーター (Ngen.exe) を使用して生成されたときの条件を指定するフラグを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCompilerFlags (
    [out] DWORD *pdwFlags
);
```

## <a name="parameters"></a>パラメーター

`pdwFlags`  
入出力JIT コンパイラまたはネイティブイメージジェネレーターの動作を指定する[CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md)列挙値へのポインター。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** CorDebug.idl、CorDebug.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
