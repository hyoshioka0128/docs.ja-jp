---
title: CorAssemblyFlags 列挙型
ms.date: 03/30/2017
api_name:
- CorAssemblyFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorAssemblyFlags
helpviewer_keywords:
- CorAssemblyFlags enumeration [.NET Framework metadata]
ms.assetid: bb8db3b6-d81d-49fc-b74c-dbc908a9eab9
topic_type:
- apiref
ms.openlocfilehash: b1a83f07f03ddb17d5c306453cf838101a77ed65
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007937"
---
# <a name="corassemblyflags-enumeration"></a>CorAssemblyFlags 列挙型
アセンブリ コンパイルに適用されるメタデータを記述する値が格納されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorAssemblyFlags {  
  
    afPublicKey             =   0x0001,  
    afPA_None               =   0x0000,  
    afPA_MSIL               =   0x0010,  
    afPA_x86                =   0x0020,  
    afPA_IA64               =   0x0030,  
    afPA_AMD64              =   0x0040,  
    afPA_ARM                =   0x0050,  
    afPA_NoPlatform         =   0x0070,  
    afPA_Specified          =   0x0080,  
    afPA_Mask               =   0x0070,  
    afPA_FullMask           =   0x00F0,  
    afPA_Shift              =   0x0004,  
  
    afEnableJITcompileTracking  =   0x8000,  
    afDisableJITcompileOptimizer=   0x4000,  
  
    afRetargetable          =   0x0100,  
    afContentType_Default        =   0x0000,  
    afContentType_WindowsRuntime =   0x0200,  
    afContentType_Mask           =   0x0E00,  
  
} CorAssemblyFlags;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`afPublicKey`|アセンブリ参照が完全なハッシュされていない公開キーを保持していることを示します。|  
|`afPA_None`|プロセッサアーキテクチャが指定されていないことを示します。|  
|`afPA_MSIL`|プロセッサアーキテクチャがニュートラル (PE32) であることを示します。|  
|`afPA_x86`|プロセッサアーキテクチャが x86 (PE32) であることを示します。|  
|`afPA_IA64`|プロセッサアーキテクチャが Itanium (PE32 +) であることを示します。|  
|`afPA_AMD64`|プロセッサアーキテクチャが AMD X64 (PE32 +) であることを示します。|  
|`afPA_ARM`|プロセッサアーキテクチャが ARM (PE32) であることを示します。|  
|`afPA_NoPlatform`|アセンブリが参照アセンブリであることを示します。つまり、アーキテクチャには適用されますが、どのアーキテクチャでも実行することはできません。 したがって、フラグはと同じ `afPA_Mask` です。|  
|`afPA_Specified`|プロセッサアーキテクチャフラグをレコードに反映する必要があることを示し `AssemblyRef` ます。|  
|`afPA_Mask`|プロセッサアーキテクチャを記述するマスク。|  
|`afPA_FullMask`|プロセッサアーキテクチャの説明を含めることを指定します。|  
|`afPA_Shift`|プロセッサアーキテクチャフラグのインデックスとの間のシフト数を示します。|  
|`afEnableJITcompileTracking`|のからの対応する値を示し <xref:System.Diagnostics.DebuggableAttribute.DebuggingModes> <xref:System.Diagnostics.DebuggableAttribute> ます。|  
|`afDisableJITcompileOptimizer`|のからの対応する値を示し <xref:System.Diagnostics.DebuggableAttribute.DebuggingModes> <xref:System.Diagnostics.DebuggableAttribute> ます。|  
|`afRetargetable`|アセンブリを実行時に別のパブリッシャーからのアセンブリに再ターゲットできることを示します。|  
|`afContentType_Mask`|コンテンツの種類を説明するマスク。|  
|`afContentType_Default`|既定のコンテンツタイプを示します。|  
|`afContentType_WindowsRuntime`|Windows ランタイムコンテンツの種類を示します。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorHdr. h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ列挙体](metadata-enumerations.md)
