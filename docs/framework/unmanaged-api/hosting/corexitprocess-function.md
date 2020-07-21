---
title: CorExitProcess 関数
ms.date: 03/30/2017
api_name:
- CorExitProcess
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CorExitProcess
helpviewer_keywords:
- CorExitProcess function [.NET Framework hosting]
ms.assetid: a5cab4c6-990e-47f3-8798-cf422b791015
topic_type:
- apiref
ms.openlocfilehash: a60805e1fd78cb14835957a7afc14fe279cb20fb
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616568"
---
# <a name="corexitprocess-function"></a>CorExitProcess 関数
現在のアンマネージ プロセスを終了します。  
  
 この関数は .NET Framework 4 で非推奨とされました。 代わりに[ICLRMetaHost:: ExitProcess](iclrmetahost-exitprocess-method.md)メソッドを使用してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void STDMETHODCALLTYPE CorExitProcess (
  int  exitCode  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `exitCode`  
 プロセス終了コードを指定する整数です。  
  
## <a name="remarks"></a>解説  
  
> [!NOTE]
> .NET Framework 4 以降では、 `CorExitProcess` レガシ api がバインドされているランタイムだけでなく、プロセスで開始されたすべてのランタイムを終了します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [非推奨の CLR ホスト関数](deprecated-clr-hosting-functions.md)
