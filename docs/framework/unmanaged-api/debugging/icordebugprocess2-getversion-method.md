---
title: ICorDebugProcess2::GetVersion メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.GetVersion
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::GetVersion
helpviewer_keywords:
- GetVersion method, ICorDebugProcess2 interface [.NET Framework debugging]
- ICorDebugProcess2::GetVersion method [.NET Framework debugging]
ms.assetid: e11d5a75-61d9-4548-aedf-79c26079bd17
topic_type:
- apiref
ms.openlocfilehash: 391b848d3b3f66f6af6bf3adbefb6e94d526e748
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213505"
---
# <a name="icordebugprocess2getversion-method"></a>ICorDebugProcess2::GetVersion メソッド

このプロセスで実行されている共通言語ランタイム (CLR) のバージョン番号を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetVersion (
    [out] COR_VERSION     *version
);
```

## <a name="parameters"></a>パラメーター

`version`\
入出力ランタイムのバージョン番号を格納する COR_VERSION 構造体へのポインター。

## <a name="remarks"></a>Remarks

`GetVersion`プロセスにランタイムが読み込まれていない場合、メソッドはエラーコードを返します。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** CorDebug.idl、CorDebug.h

**ライブラリ:** CorGuids.lib

**.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
