---
title: ESymbolReadingPolicy 列挙型
ms.date: 03/30/2017
api_name:
- ESymbolReadingPolicy
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ESymbolReadingPolicy
helpviewer_keywords:
- ESymbolReadingPolicy enumeration [.NET Framework hosting]
ms.assetid: 4dc6c80d-b694-480b-a378-d5b18420ce17
topic_type:
- apiref
ms.openlocfilehash: 5c3d1d0ebc56ee93c950afb4f015c8e10ec6a0f7
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616178"
---
# <a name="esymbolreadingpolicy-enumeration"></a>ESymbolReadingPolicy 列挙型
プログラムデータベース (PDB) ファイルを読み取るためのポリシーを設定する値が含まれます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum {  
    eSymbolReadingNever,  
    eSymbolReadingAlways,  
    eSymbolReadingFullTrustOnly  
} ESymbolReadingPolicy;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`eSymbolReadingAlways`|デバッガーが常に PDB ファイルを読み取る必要があることを指定します。|  
|`eSymbolReadingFullTrustOnly`|デバッガーが、完全に信頼されたアセンブリに関連付けられている PDB ファイルのみを読み取るように指定します。|  
|`eSymbolReadingNever`|デバッガーが PDB ファイルを読み取らないように指定します。|  
  
## <a name="remarks"></a>解説  
 `ESymbolReadingPolicy`列挙体は、 [ICLRDebugManager:: SetSymbolReadingPolicy](iclrdebugmanager-setsymbolreadingpolicy-method.md)メソッドと共に使用されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスティングの列挙体](hosting-enumerations.md)
