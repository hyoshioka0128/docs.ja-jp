---
title: ICorDebugModule2::ResolveAssembly メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.ResolveAssembly
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::ResolveAssembly
helpviewer_keywords:
- ICorDebugModule2::ResolveAssembly method [.NET Framework debugging]
- ResolveAssembly method [.NET Framework debugging]
ms.assetid: ddf9085c-7161-44bd-9609-cd2732b9009f
topic_type:
- apiref
ms.openlocfilehash: e64e39d10d20f63430ffe9d2c4df8643e286a677
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210036"
---
# <a name="icordebugmodule2resolveassembly-method"></a>ICorDebugModule2::ResolveAssembly メソッド

指定したメタデータトークンによって参照されるアセンブリを解決します。

## <a name="syntax"></a>構文

```cpp
HRESULT ResolveAssembly (
    [in]  mdToken             tkAssemblyRef,
    [out] ICorDebugAssembly   **ppAssembly
);
```

## <a name="parameters"></a>パラメーター

`tkAssemblyRef`\
から`mdToken`アセンブリを参照する値。

`ppAssembly`\
入出力アセンブリを表す、オブジェクトのアドレスへのポインター。

## <a name="remarks"></a>Remarks

が呼び出されたときにアセンブリがまだ読み込まれていない場合は `ResolveAssembly` 、CORDBG_E_CANNOT_RESOLVE_ASSEMBLY の HRESULT 値が返されます。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** CorDebug.idl、CorDebug.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
