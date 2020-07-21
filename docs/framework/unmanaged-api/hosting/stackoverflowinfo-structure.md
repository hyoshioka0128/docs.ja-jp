---
title: StackOverflowInfo 構造体
ms.date: 03/30/2017
api_name:
- StackOverflowInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- StackOverflowInfo
helpviewer_keywords:
- StackOverflowInfo structure [.NET Framework hosting]
ms.assetid: 519389f2-0217-436c-99d4-93a76ebce5b5
topic_type:
- apiref
ms.openlocfilehash: 941093b9a0856c2b716ba359c854473f3c9ea26a
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84006520"
---
# <a name="stackoverflowinfo-structure"></a>StackOverflowInfo 構造体
発生したオーバーフローの種類とオーバーフローによってスローされた例外に関する情報を格納します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct _StackOverflowInfo {  
    StackOverflowType   soType;  
    EXCEPTION_POINTERS  *pExceptionInfo;  
} StackOverflowInfo;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`soType`|オーバーフローの種類を指定する[StackOverflowType](stackoverflowtype-enumeration.md)列挙体の値。|  
|`pExceptionInfo`|Win32 オブジェクトへのポインター。このオブジェクトには、例外 `EXCEPTION_POINTERS` のコンピューターに依存しない記述と、例外の発生時にプロセッサコンテキストのコンピューターに依存する記述を持つコンテキストレコードが含まれています。|  
  
## <a name="remarks"></a>コメント  
 `StackOverflowInfo`オブジェクトは、イベントの[Iactiononclrevent:: OnEvent](iactiononclrevent-onevent-method.md)メソッドに渡され `Event_StackOverflow` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ホスト構造体](hosting-structures.md)
