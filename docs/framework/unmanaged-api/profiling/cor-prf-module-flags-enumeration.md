---
title: COR_PRF_MODULE_FLAGS 列挙体
ms.date: 03/30/2017
api_name:
- COR_PRF_MODULE_FLAGS
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_MODULE_FLAGS
helpviewer_keywords:
- COR_PRF_MODULE_FLAGS enumeration [.NET Framework profiling]
ms.assetid: 7bc3a938-0df1-4739-9ff1-89cff454b704
topic_type:
- apiref
ms.openlocfilehash: 12e7faa8d9fee7698de9d9734f522d818f225c84
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500820"
---
# <a name="cor_prf_module_flags-enumeration"></a>COR_PRF_MODULE_FLAGS 列挙体
モジュールのプロパティを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum  
{  
    COR_PRF_MODULE_DISK             = 0x00000001,  
    COR_PRF_MODULE_NGEN             = 0x00000002,  
    COR_PRF_MODULE_DYNAMIC          = 0x00000004,  
    COR_PRF_MODULE_COLLECTIBLE      = 0x00000008,  
    COR_PRF_MODULE_RESOURCE         = 0x00000010,  
    COR_PRF_MODULE_FLAT_LAYOUT      = 0x00000020,  
    COR_PRF_MODULE_WINDOWS_RUNTIME  = 0x00000040  
}   COR_PRF_MODULE_FLAGS;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|COR_PRF_MODULE_DISK|モジュールはディスクから読み込まれました。|  
|COR_PRF_MODULE_NGEN|モジュールは、ネイティブイメージジェネレーター (Ngen.exe) によって生成されました。|  
|COR_PRF_MODULE_DYNAMIC|モジュールは、名前空間のメソッドによって作成されました <xref:System.Reflection.Emit?displayProperty=nameWithType> 。|  
|COR_PRF_MODULE_COLLECTIBLE|モジュールの有効期間は、ガベージコレクターによって管理されます。|  
|COR_PRF_MODULE_RESOURCE|モジュールにはメタデータが含まれておらず、厳密にリソースとして使用されます。 このビットに相当するマネージドは <xref:System.Reflection.Module.IsResource%2A?displayProperty=nameWithType> メソッドです。|  
|COR_PRF_MODULE_FLAT_LAYOUT|メモリ内のモジュールのレイアウトはフラットであり、マップされていません。 モジュールにこのビットが設定されている場合、移植可能な実行可能 (PE) ファイルヘッダーから情報を直接読み取るプロファイラーは、ヘッダーの相対仮想アドレス (RVAs) を解釈する際に注意する必要があります。|  
|COR_PRF_MODULE_WINDOWS_RUNTIME|Windows ランタイム content type フラグが、このモジュールのアセンブリのメタデータで設定されています。 これは、すべての Windows メタデータ (winmd) モジュールに当てはまります。|  
  
## <a name="remarks"></a>解説  
 COR_PRF_MODULE_FLAGS のビットは、 `pdwModuleFlags` [ICorProfilerInfo3:: GetModuleInfo2](icorprofilerinfo3-getmoduleinfo2-method.md)メソッドの output パラメーターでプロファイラーに返されます。 複数のフラグの組み合わせが可能ですが、すべての組み合わせが可能であるとは限りません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [列挙体のプロファイリング](profiling-enumerations.md)
