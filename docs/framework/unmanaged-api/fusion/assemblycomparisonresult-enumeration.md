---
title: AssemblyComparisonResult 列挙型
ms.date: 03/30/2017
api_name:
- AssemblyComparisonResult
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- AssemblyComparisonResult
helpviewer_keywords:
- AssemblyComparisonResult enumeration [.NET Framework fusion]
ms.assetid: bd042f89-10b1-40ca-946e-46da082f5263
topic_type:
- apiref
ms.openlocfilehash: e3cdb648397ca4f4aa2326e4f2349a5a14c3edcc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79178290"
---
# <a name="assemblycomparisonresult-enumeration"></a>AssemblyComparisonResult 列挙型
[2](compareassemblyidentity-function.md)つのアセンブリ ID の等価性を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
typedef enum _tagAssemblyComparisonResult {  
    ACR_Unknown,
    ACR_EquivalentFullMatch,  
    ACR_EquivalentWeakNamed,  
    ACR_EquivalentFXUnified,  
    ACR_EquivalentUnified,
    ACR_NonEquivalentVersion,  
    ACR_NonEquivalent,
    ACR_EquivalentPartialMatch,  
    ACR_EquivalentPartialWeakNamed,
    ACR_EquivalentPartialUnified,  
    ACR_EquivalentPartialFXUnified,  
    ACR_NonEquivalentPartialVersion
} AssemblyComparisonResult;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー名|説明|  
|-----------------|-----------------|  
|`ACR_EquivalentFullMatch`|比較内のすべてのアセンブリ フィールドが一致することを示します。|  
|`ACR_EquivalentFXUnified`|.NET Framework バージョン 2.0 のアセンブリ バージョン番号の共通言語ランタイム バージョン (CLR) の統一に基づいて、アセンブリが等価と見なされることを示します。|  
|`ACR_EquivalentPartialFXUnified`|.NET Framework 2.0 のアセンブリ バージョン番号の CLR 統合に基づいて、アセンブリの部分的な一致を示します。|  
|`ACR_EquivalentPartialMatch`|アセンブリの部分的な一致を示します。|  
|`ACR_EquivalentPartialUnified`|バージョン番号のレガシ統一に基づいてアセンブリの部分的一致を示します。|  
|`ACR_EquivalentPartialWeakNamed`|名前付きのアセンブリの部分一致を示します。|  
|`ACR_EquivalentUnified`|アセンブリが、.NET Framework のレガシ バージョンのバージョン番号の CLR 統合に基づいて等価であると見なされることを示します。|  
|`ACR_EquivalentWeakNamed`|バージョン番号が無視された 2 つの単純な名前付きアセンブリ間の一致を示します。|  
|`ACR_NonEquivalent`|2 つのアセンブリ間で一致が発生しなかった場合を示します。|  
|`ACR_NonEquivalentPartialVersion`|バージョン番号が部分的にしか一致しない場合は、2 つのアセンブリが一致することを示します。|  
|`ACR_NonEquivalentVersion`|2 つのアセンブリが、バージョン番号が一致しない場合を除いて一致することを示します。|  
|`ACR_Unknown`|非等価性の理由が不明であることを示します。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** フュージョン.h  
  
 **ライブラリ:** MsCorEE.dll にリソースとして含まれる  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [CompareAssemblyIdentity 関数](compareassemblyidentity-function.md)
- [fusion 列挙体](fusion-enumerations.md)
