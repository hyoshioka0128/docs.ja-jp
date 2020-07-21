---
title: COR_NATIVE_LINK 構造体
ms.date: 03/30/2017
api_name:
- COR_NATIVE_LINK
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_NATIVE_LINK
helpviewer_keywords:
- COR_NATIVE_LINK structure [.NET Framework metadata]
ms.assetid: 6ef78d3c-1c69-4141-b687-dcb065b7a74d
topic_type:
- apiref
ms.openlocfilehash: a11b7d5939c4c20504b1ff3dfb4613f85bca0db4
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007976"
---
# <a name="cor_native_link-structure"></a>COR_NATIVE_LINK 構造体
ネイティブ コードのリンクに使用される情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct
{  
    BYTE        m_linkType;  
    BYTE        m_flags;  
    mdMemberRef m_entryPoint;  
} COR_NATIVE_LINK;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`m_linkType`|ネイティブコードでリンクされる型。 この値は、 [CorNativeLinkType](cornativelinktype-enumeration.md)値の1つです。|  
|`m_flags`|ネイティブコードをリンクするときにリンカーによって使用されるフラグ。 この値は、 [CorNativeLinkFlags](cornativelinkflags-enumeration.md)値の1つです。|  
|`m_entryPoint`|エントリポイントを表す MemberRef メタデータトークン。 形式は `lib:entrypoint` です。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ構造体](metadata-structures.md)
- [CorNativeLinkType 列挙型](cornativelinktype-enumeration.md)
- [CorNativeLinkFlags 列挙型](cornativelinkflags-enumeration.md)
