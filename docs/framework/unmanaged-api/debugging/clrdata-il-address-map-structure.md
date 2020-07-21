---
title: CLRDATA_IL_ADDRESS_MAP 構造体
ms.date: 01/16/2019
api.name:
- CLRDATA_IL_ADDRESS_MAP Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- CLRDATA_IL_ADDRESS_MAP Structure
helpviewer.keywords:
- CLRDATA_IL_ADDRESS_MAP Structure [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: e680a7a0dc3209d1988f6c84be0864572a74b3a4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179371"
---
# <a name="clrdata_il_address_map-structure"></a>CLRDATA_IL_ADDRESS_MAP 構造体

IL からアドレスマッピングを定義します。

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>構文

```cpp
typedef struct
{
    ULONG32 ilOffset;
    CLRDATA_ADDRESS startAddress;
    CLRDATA_ADDRESS endAddress;
    CLRDataSourceType type;
} CLRDATA_IL_ADDRESS_MAP;
```

## <a name="members"></a>メンバー

| メンバー         | 説明                                            |
| -------------- | ------------------------------------------------------ |
| `ilOffset`     | 含まれるアドレス範囲の IL オフセット              |
| `startAddress` | 範囲の開始アドレス。                        |
| `endAddress`   | 範囲の終了アドレス。                          |
| `type`         | データの型。 この値は現在使用されていません |

## <a name="remarks"></a>解説

この構造体はランタイム内に存在し、ヘッダーやライブラリ ファイルを通じて公開されません。 これを使用するには、上記で指定した構造体を定義します`CLRDATA_ADDRESS`。

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
**ヘッダー:** なし  
**ライブラリ:** なし **.NET フレームワークのバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [列挙型](clrdatasourcetype-enumeration.md)
- [デバッグ](index.md)
- [デバッグ構造体](debugging-structures.md)
