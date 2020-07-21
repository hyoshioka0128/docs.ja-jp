---
title: ICorDebugProcess4 インターフェイス
ms.date: 02/07/2019
api_name:
- ICorDebugProcess4
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess4
helpviewer_keywords:
- ICorDebugProcess4 interface [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: fcf725ea98fa4351e72cf592f92968ee2233ecb0
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213583"
---
# <a name="icordebugprocess4-interface"></a>ICorDebugProcess4 インターフェイス

アウトプロセス実行制御のサポートを提供します。

## <a name="methods"></a>メソッド

| メソッド                                                                 | 説明                                                                                             |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| [ProcessStateChanged](icordebugprocess4-processstatechanged-method.md) | アウトプロセスデバッガーがデバッグ対象の実行を継続していることを ICorDebug パイプラインに通知します。 |

## <a name="remarks"></a>Remarks

このインターフェイスはランタイム内に存在し、ヘッダーまたはライブラリファイルを介して公開されることはありません。 ただし、これは、 `IUnknown` `E930C679-78AF-4953-8AB7-B0AABF0F9F80` 通常の com 機構を通じて取得できる GUID を使用してから派生する com インターフェイスです。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** 存在

**ライブラリ:** 存在

**.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
