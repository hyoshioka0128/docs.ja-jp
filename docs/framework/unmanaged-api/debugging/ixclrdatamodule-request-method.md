---
title: 'IXCLRDataModule:: Request メソッド'
ms.date: 01/16/2019
api.name:
- IXCLRDataModule::Request Method
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataModule::Request Method
helpviewer.keywords:
- IXCLRDataModule::Request Method [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: 3c18fc5c947cbb89fc4e9aed60d3cedcbe22d749
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83420813"
---
# <a name="ixclrdatamodulerequest-method"></a>IXCLRDataModule:: Request メソッド

モジュールのデータで指定されたバッファーへの読み込みを要求します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT Request([in] ULONG32 reqCode,
    [in] ULONG32 inBufferSize,
    [in, size_is(inBufferSize)] BYTE* inBuffer,
    [in] ULONG32 outBufferSize,
    [out, size_is(outBufferSize)] BYTE* outBuffer);
```

## <a name="parameters"></a>パラメーター

`reqCode`\
から送信される要求の種類。

`inBufferSize`\
[in] 渡される入力バッファーのサイズ。

`inBuffer`\
[in、size_is (inBufferSize)]要求で送信される生データのバッファーポインター。

`outBufferSize`\
から出力バッファーのサイズ。

`outBuffer`\
[out、size_is (outBufferSize)]要求応答を格納するために使用するバッファーポインター。

## <a name="remarks"></a>解説

指定されたメソッドはインターフェイスの一部で `IXCLRDataModule` あり、仮想メソッドテーブルの37th スロットに対応します。

## <a name="requirements"></a>要件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。
**ヘッダー:** None **Library:** None **.NET Framework バージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [IXCLRDataModule インターフェイス](ixclrdatamodule-interface.md)
