---
title: AssemblyRefFlags 列挙型
ms.date: 03/30/2017
api_name:
- AssemblyRefFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- AssemblyRefFlags
helpviewer_keywords:
- AssemblyRefFlags enumeration [.NET Framework metadata]
ms.assetid: decd4f46-f3b2-466f-9501-e74f2b86b846
topic_type:
- apiref
ms.openlocfilehash: 1307f555c9d8b6d28febcf25db89ae856c143d71
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009406"
---
# <a name="assemblyrefflags-enumeration"></a>AssemblyRefFlags 列挙型
アセンブリ参照の機能を記述する値を格納します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    arfFullOriginator = 0x0001  
} AssemblyRefFlags;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`arfFullOriginator`|アセンブリ参照に、アセンブリの発行者に関する完全なハッシュされていない情報が含まれることを指定します。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ列挙体](metadata-enumerations.md)
- [IMetaDataAssemblyEmit インターフェイス](imetadataassemblyemit-interface.md)
- [DefineAssemblyRef メソッド](imetadataassemblyemit-defineassemblyref-method.md)
