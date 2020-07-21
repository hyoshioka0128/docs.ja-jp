---
title: CustomDumpItem 構造体
ms.date: 03/30/2017
api_name:
- CustomDumpItem
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CustomDumpItem
helpviewer_keywords:
- CustomDumpItem structure [.NET Framework hosting]
ms.assetid: fd9085ff-7beb-4c38-97f0-037cd8ba4f65
topic_type:
- apiref
ms.openlocfilehash: 5c77a332593ba470d2e29b87cba182a770d5db7e
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616438"
---
# <a name="customdumpitem-structure"></a>CustomDumpItem 構造体
エラー報告のカスタムダンプに追加するアイテムについて説明します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
struct {  
    ECustomDumpItemKind itemKind;
    union {  
        UINT_PTR pReserved;  
    }  
} CustomDumpItem;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`itemKind`|追加する項目の種類を示す[ECustomDumpItemKind](ecustomdumpitemkind-enumeration.md)値。|  
|`pReserved`|現在は使用しません。 共用体に追加された項目は、ポインターサイズ以下である必要があります。 `struct`が必要な場合は、それを個別に割り当てて、それをポイントする必要があります。|  
  
## <a name="remarks"></a>解説  
 [ICLRErrorReportingManager:: BeginCustomDump](iclrerrorreportingmanager-begincustomdump-method.md)は、型のパラメーターを受け取り `CustomDumpItem` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト構造体](hosting-structures.md)
