---
title: CorThreadSafetyOptions 列挙型
ms.date: 03/30/2017
api_name:
- CorThreadSafetyOptions
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorThreadSafetyOptions
helpviewer_keywords:
- CorThreadSafetyOptions enumeration [.NET Framework metadata]
ms.assetid: dae07d9b-df51-488c-b17e-52d6e48217bd
topic_type:
- apiref
ms.openlocfilehash: 8c0527a7bc3cde7344bf809dc8e6f5a3fac04852
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007508"
---
# <a name="corthreadsafetyoptions-enumeration"></a>CorThreadSafetyOptions 列挙型

スレッド セーフのオプションを選択するためのフラグを指定します。

## <a name="syntax"></a>構文

```cpp
typedef enum CorThreadSafetyOptions {
    MDThreadSafetyDefault       = 0x00000000,
    MDThreadSafetyOff           = 0x00000000,
    MDThreadSafetyOn            = 0x00000001,
} CorThreadSafetyOptions;
```

## <a name="members"></a>メンバー

|メンバー|説明|
|------------|-----------------|
|`MDThreadSafetyDefault`|既定値です。 `MDThreadSafetyOff` と同じ。|
|`MDThreadSafetyOff`|リーダー/ライターロックを設定できないことを示します。|
|`MDThreadSafetyOn`|リーダー/ライターロックを設定できることを示します。|

## <a name="requirements"></a>必要条件

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

**ヘッダー:** CorHdr. h

**.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>関連項目

- [メタデータ列挙体](metadata-enumerations.md)
