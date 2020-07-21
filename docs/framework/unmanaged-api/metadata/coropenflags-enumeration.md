---
title: CorOpenFlags 列挙型
ms.date: 03/30/2017
api_name:
- CorOpenFlags
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorOpenFlags
helpviewer_keywords:
- CorOpenFlags enumeration [.NET Framework metadata]
ms.assetid: e27a83b5-2698-4996-9032-1e0fed8b91ca
topic_type:
- apiref
ms.openlocfilehash: 7318a7ea3eb1ddb047a799e58ebdfd9ce6cd76d1
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "84007586"
---
# <a name="coropenflags-enumeration"></a>CorOpenFlags 列挙型
マニフェスト ファイルを開くときにメタデータの動作を制御するフラグ値を含めます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum CorOpenFlags  
{  
    ofRead              =   0x00000000,  
    ofWrite             =   0x00000001,  
    ofReadWriteMask     =   0x00000001,  
    ofCopyMemory        =   0x00000002,  
    ofCacheImage        =   0x00000004,  
    ofManifestMetadata  =   0x00000008,  
    ofReadOnly          =   0x00000010,  
    ofTakeOwnership     =   0x00000020,  
    ofCacheImage        =   0x00000004,  
    ofNoTypeLib         =   0x00000080,  
    ofNoTransform       =   0x00001000,  
    ofReserved1         =   0x00000100,  
    ofReserved2         =   0x00000200,  
    ofReserved          =   0xffffff40  
} CorOpenFlags;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`ofRead`|ファイルが読み取り専用で開かれることを示します。|  
|`ofWrite`|ファイルが書き込み用に開かれることを示します。<br /><br /> .winmd ファイルを開くときに `ofWrite` フラグを使用する場合は、`ofNoTransform` フラグも渡す必要があります。|  
|`ofReadWriteMask`|読み取りおよび書き込み用のマスク。|  
|`ofCopyMemory`|ファイルがメモリ内に読み込まれることを示します。 メタデータは自身のコピーを保持する必要があります。|  
|`ofCacheImage`|互換性のために残されています。 このフラグは無視されます。|  
|`ofManifestMetadata`|互換性のために残されています。 このフラグは無視されます。|  
|`ofReadOnly`|は、ファイルを読み取り用に開く必要があること、および IMetaDataEmit に対するの呼び出しを行うことができないことを示し `QueryInterface` ます。 [IMetaDataEmit](imetadataemit-interface.md)|  
|`ofTakeOwnership`|[CoTaskMemAlloc](/windows/desktop/api/combaseapi/nf-combaseapi-cotaskmemalloc)への呼び出しを使用してメモリが割り当てられ、メタデータによって解放されることを示します。|  
|`ofNoTypeLib`|互換性のために残されています。 このフラグは無視されます。|  
|`ofNoTransform`|.winmd ファイルの自動変換を無効にする必要があることを示します。 つまり、Windows Runtime タイプから .NET Framework タイプへの投射は無効になります。 詳細については、「 [Windows ランタイムと CLR-.net と Windows ランタイム](https://docs.microsoft.com/archive/msdn-magazine/2012/windows-8-special-issue/windows-runtime-and-the-clr-underneath-the-hood-with-net-and-the-windows-runtime)」を参照してください。|  
|`ofReserved1`|内部使用のために予約されています。|  
|`ofReserved2`|内部使用のために予約されています。|  
|`ofReserved`|内部使用のために予約されています。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorHdr. h  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ列挙体](metadata-enumerations.md)
