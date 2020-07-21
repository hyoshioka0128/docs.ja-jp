---
title: ASSEMBLYMETADATA 構造体
ms.date: 03/30/2017
api_name:
- ASSEMBLYMETADATA
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ASSEMBLYMETADATA
helpviewer_keywords:
- ASSEMBLYMETADATA structure [.NET Framework metadata]
ms.assetid: 1af98e57-9145-4d35-bb78-77d1da7c91a5
topic_type:
- apiref
ms.openlocfilehash: 5c7211fc2523b70313a1e4d4d9d2da0dcecd1d32
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84009432"
---
# <a name="assemblymetadata-structure"></a>ASSEMBLYMETADATA 構造体
バージョン、ロケール、プロセッサ、オペレーティングシステムのサポートレベルなど、参照されるアセンブリに関する情報を格納します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef struct {  
    USHORT  usMajorVersion;  
    USHORT  usMinorVersion;  
    USHORT  usBuildNumber;  
    USHORT  usRevisionNumber;  
    LPWSTR  szLocale;  
    ULONG   cbLocale;  
    DWORD*  rdwProcessor[];  
    ULONG   ulProcessor  
    OSINFO* rOS[];  
    ULONG   ulOS;  
} ASSEMBLYMETADATA;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`usMajorVersion`|参照アセンブリのメジャーバージョン番号。 この値を0にすることはできません。 のすべてのビットが設定されている場合は、 `usMajorVersion` メジャーバージョンが指定されていません。|  
|`usMinorVersion`|参照アセンブリのマイナーバージョン番号。 この値を0にすることはできません。 のすべてのビットが設定されている場合は、 `usMinorVersion` マイナーバージョンが指定されていません。|  
|`usBuildNumber`|参照アセンブリのビルド番号。 この値を0にすることはできません。 のすべてのビットが設定されている場合は、 `usBuildNumber` ビルド番号が指定されていません。|  
|`usRevisionNumber`|参照アセンブリのリビジョン番号。 この値を0にすることはできません。 のすべてのビットが設定されている場合は、 `usRevisionNumber` リビジョン番号が指定されていません。|  
|`szLocale`|RFC1766 仕様に準拠しているロケール名のリスト。セミコロンで区切られ、参照アセンブリによってサポートされるロケールを指定します。 Null 値は、ロケールに依存しないことを示します。 **注:** .NET Framework バージョン1.0 では、複数のロケールを指定することはできません。|  
|`cbLocale`|のワイド文字のサイズ `szLocale` 。|  
|`rdwProcessor`|参照アセンブリでサポートされているプロセッサの種類について、Winnt.h で定義されている識別子の配列。 NULL 値は、プロセッサに依存しないことを示します。|  
|`ulProcessor`|`rdwProcessor` 配列の長さ。|  
|`rOS`|参照アセンブリによってサポートされているオペレーティングシステムを指定する[Osinfo](osinfo-structure.md)インスタンスの配列。 NULL 値は、オペレーティングシステムに依存しないことを示します。|  
|`ulOS`|`rOS` 配列の長さ。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll のリソースとして使用されます。  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ構造体](metadata-structures.md)
- [IMetaDataAssemblyEmit インターフェイス](imetadataassemblyemit-interface.md)
- [OSINFO 構造体](osinfo-structure.md)
