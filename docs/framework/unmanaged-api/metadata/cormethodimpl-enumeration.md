---
title: CorMethodImpl 列挙型
ms.date: 03/30/2017
api_name:
- CorMethodImpl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorMethodImpl
helpviewer_keywords:
- CorMethodImpl enumeration [.NET Framework metadata]
ms.assetid: ffbb3caf-20da-4a4b-8983-77376e72b990
topic_type:
- apiref
ms.openlocfilehash: b32e8f0b03ef6d550c384f3d932cc295a7270028
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007664"
---
# <a name="cormethodimpl-enumeration"></a>CorMethodImpl 列挙型
メソッド実装の機能を記述する値が格納されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorMethodImpl {  
  
    miCodeTypeMask      =   0x0003,  
    miIL                =   0x0000,  
    miNative            =   0x0001,  
    miOPTIL             =   0x0002,  
    miRuntime           =   0x0003,  
  
    miManagedMask       =   0x0004,  
    miUnmanaged         =   0x0004,  
    miManaged           =   0x0000,  
  
    miForwardRef        =   0x0010,  
    miPreserveSig       =   0x0080,  
  
    miInternalCall      =   0x1000,  
    miSynchronized      =   0x0020,  
    miNoInlining        =   0x0008,  
    miAggressiveInlining =  0x0100,  
    miNoOptimization     =  0x0040,  
    miMaxMethodImplVal  =   0xffff  
  
} CorMethodImpl;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`miCodeTypeMask`|コードの種類を記述するフラグ。|  
|`miIL`|メソッドの実装が Microsoft 中間言語 (MSIL) であることを指定します。|  
|`miNative`|メソッド実装がネイティブであることを指定します。|  
|`miOPTIL`|メソッドの実装が OPTIL であることを指定します。|  
|`miRuntime`|メソッドの実装が共通言語ランタイムによって提供されることを指定します。|  
|`miManagedMask`|コードがマネージとアンマネージのどちらであるかを示すフラグ。|  
|`miUnmanaged`|メソッドの実装がアンマネージであることを指定します。|  
|`miManaged`|メソッドの実装が管理されることを指定します。|  
|`miForwardRef`|メソッドが定義されていることを指定します。 このフラグは、主にマージシナリオで使用されます。|  
|`miPreserveSig`|HRESULT 変換のメソッドシグネチャを破損させることができないことを指定します。|  
|`miInternalCall`|共通言語ランタイムによる内部使用のために予約されています。|  
|`miSynchronized`|メソッドがその本体を通じてシングルスレッドであることを指定します。|  
|`miNoInlining`|メソッドがインライン化できないことを指定します。|  
|`miAggressiveInlining`|可能な場合は、メソッドをインライン展開することを指定します。|  
|`miNoOptimization`|メソッドを最適化しないことを指定します。|  
|`miMaxMethodImplVal`|の最大有効値 `CorMethodImpl` 。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorHdr. h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ列挙体](metadata-enumerations.md)
