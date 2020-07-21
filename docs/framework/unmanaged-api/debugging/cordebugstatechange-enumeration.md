---
title: CorDebugStateChange 列挙体
ms.date: 02/07/2019
api_name:
- CorDebugStateChange
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 1d4424ab-5143-4e50-a84a-ceeb4ddf3bba
topic_type:
- apiref
ms.openlocfilehash: d94422d25da91cd2a6653a95cbd852c3930a151a
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795691"
---
# <a name="cordebugstatechange-enumeration"></a>CorDebugStateChange 列挙体

プロセスへの変更に基づいて破棄が必要となった、キャッシュされたデータの量を示します。

## <a name="syntax"></a>構文

```cpp
typedef enum CorDebugStateChange
{
    PROCESS_RUNNING = 0x0000001,
    FLUSH_ALL       = 0x0000002,
} CorDebugStateChange;
```

## <a name="members"></a>メンバー

| メンバー            | 説明                                                              |
| ----------------- | ------------------------------------------------------------------------ |
| `PROCESS_RUNNING` | プロセスはフォワード実行によって新しいメモリ状態に達しています。            |
| `FLUSH_ALL`       | プロセスのメモリは、以前とは異なる状態になっている場合があります。 |

## <a name="remarks"></a>Remarks

 デバッガーが[ICorDebugProcess4::P rocessstatechanged](icordebugprocess4-processstatechanged-method.md)または[ICorDebugProcess6::P rocessstatechanged](icordebugprocess6-processstatechanged-method.md)を使用し`ProcessStateChanged`てメソッドを呼び出すと、 `CorDebugStateChange`列挙体のメンバーが引数として提供されます。

## <a name="requirements"></a>必要条件

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

 **ヘッダー:** CorDebug.idl、CorDebug.h

 **ライブラリ:** CorGuids.lib

 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v20plus-md.md)]

## <a name="see-also"></a>関連項目

- [列挙体のデバッグ](debugging-enumerations.md)
- [デバッグ](index.md)
