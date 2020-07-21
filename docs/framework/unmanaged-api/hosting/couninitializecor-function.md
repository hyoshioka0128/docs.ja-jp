---
title: CoUninitializeCor 関数
ms.date: 03/30/2017
api_name:
- CoUninitializeCor
api_location:
- mscoree.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoUninitializeCor
helpviewer_keywords:
- CoUninitializeCor function [.NET Framework hosting]
ms.assetid: 50a95b8b-9766-470e-bb29-2c7ecddfd4a1
topic_type:
- apiref
ms.openlocfilehash: 8a8c2764398d737192190f91646d45f4edf3a0e4
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616479"
---
# <a name="couninitializecor-function"></a>CoUninitializeCor 関数
`CoUninitializeCor` は互換性のために残されています。  
  
## <a name="syntax"></a>構文  
  
```cpp  
STDAPI_(void) CoUninitializeCor(void);  
```  
  
## <a name="remarks"></a>解説  
 共通言語ランタイムをプロセスからアンロードすることはできません。 実行中のプロセスからランタイムを完全に削除するには、そのプロセスをシャットダウンする必要があります。  
  
## <a name="see-also"></a>関連項目

- [メタデータ グローバル静的関数](../metadata/metadata-global-static-functions.md)
