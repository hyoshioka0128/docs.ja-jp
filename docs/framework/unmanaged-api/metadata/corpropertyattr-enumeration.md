---
title: CorPropertyAttr 列挙型
ms.date: 03/30/2017
api_name:
- CorPropertyAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorPropertyAttr
helpviewer_keywords:
- CorPropertyAttr enumeration [.NET Framework metadata]
ms.assetid: 58ac8202-854d-4efd-acfb-d2da8b446e12
topic_type:
- apiref
ms.openlocfilehash: b6651f30e0df3a5ffc29d310b9067e76761dcf01
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007534"
---
# <a name="corpropertyattr-enumeration"></a>CorPropertyAttr 列挙型
プロパティのメタデータを記述する値が格納されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorPropertyAttr {  
  
    prSpecialName           =   0x0200,
    prReservedMask          =   0xf400,  
    prRTSpecialName         =   0x0400,  
    prHasDefault            =   0x1000,  
    prUnused                =   0xe9ff  
  
} CorPropertyAttr;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`prSpecialName`|プロパティが特別であり、その名前がどのように説明するかを指定します。|  
|`prReservedMask`|共通言語ランタイムによる内部使用のために予約されています。|  
|`prRTSpecialName`|共通言語ランタイムメタデータの内部 Api がプロパティ名のエンコーディングを確認する必要があることを指定します。|  
|`prHasDefault`|プロパティが既定値を持つことを指定します。|  
|`prUnused`|未使用。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorHdr. h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ列挙体](metadata-enumerations.md)
