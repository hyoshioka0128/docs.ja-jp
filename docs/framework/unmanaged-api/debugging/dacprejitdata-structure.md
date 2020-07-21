---
title: DacpReJitData 構造体
ms.date: 02/01/2019
api.name:
- DacpReJitData Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpReJitData Structure
helpviewer.keywords:
- DacpReJitData Structure [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 4436ece72b0a6a405fc41cba5413093fc42ce750
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860779"
---
# <a name="dacprejitdata-structure"></a>DacpReJitData 構造体

プロファイラーによってインストルメント化された特定のメソッドに関する基本情報を定義します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
struct MSLAYOUT DacpReJitData
{
    enum Flags
    {
        kUnknown,
        kRequested,
        kActive,
        kReverted,
    };

    CLRDATA_ADDRESS                 rejitID;
    Flags                           flags;
    CLRDATA_ADDRESS                 NativeCodeAddr;
};
```

## <a name="members"></a>メンバー

| メンバー           | 説明                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------ |
| `rejitID`        | メソッドの ReJit リビジョン番号。                                                          |
| `flags`          | 指定されたバージョンのメソッドの ReJit インストルメンテーションの現在の状態を示すフラグ。 |
| `NativeCodeAddr` | メソッドの rejitted 実装のベースアドレス。                                         |

## <a name="remarks"></a>解説

この構造体はランタイム内に存在し、ヘッダーまたはライブラリファイルを介して公開されることはありません。 これを使用するには、前に示したように構造体を定義します。 Microsoft コンパイラを使用してい`ms_struct`ない場合は、パッキングを使用して構造体を定義する必要もあります。

## <a name="requirements"></a>必要条件
**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** 存在  
**ライブラリ:** 存在  
**.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [デバッグ](index.md)
- [デバッグ構造体](debugging-structures.md)
