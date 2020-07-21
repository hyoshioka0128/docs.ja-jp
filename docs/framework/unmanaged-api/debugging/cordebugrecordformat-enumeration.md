---
title: CorDebugRecordFormat 列挙体
ms.date: 03/30/2017
api_name:
- CorDebugRecordFormat
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: d680c1c0-16ab-4ccc-9444-39cf8e0e05ee
topic_type:
- apiref
ms.openlocfilehash: cfbd856c73ab10642a7cf7c16cfb2d70e7fe9756
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795730"
---
# <a name="cordebugrecordformat-enumeration"></a>CorDebugRecordFormat 列挙体
ネイティブ例外デバッグ イベントに関する情報を格納するバイト配列内のデータの形式を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorDebugRecordFormat {  
    FORMAT_WINDOWS_EXCEPTIONRECORD32 = 1,  
    FORMAT_WINDOWS_EXCEPTIONRECORD64 = 2,  
} CorDebugRecordFormat;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`FORMAT_WINDOWS_EXCEPTIONRECORD32`|データは、32 ビット Windows 例外レコードです。|  
|`FORMAT_WINDOWS_EXCEPTIONRECORD64`|データは、64 ビット Windows 例外レコードです。|  
  
## <a name="remarks"></a>Remarks  
 列挙体のメンバーは、 `pRecord`引数のバイト配列の形式を示すために、 [DecodeEvent](icordebugprocess6-decodeevent-method.md)メソッドに渡されます。 `CorDebugRecordFormat`  
  
> [!NOTE]
> この列挙型は .NET ネイティブのデバッグ シナリオのみで使用することを目的としています。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のデバッグ](debugging-enumerations.md)
