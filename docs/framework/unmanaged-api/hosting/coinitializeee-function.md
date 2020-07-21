---
title: CoInitializeEE 関数
ms.date: 03/30/2017
api_name:
- CoInitializeEE
api_location:
- mscoree.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CoInitializeEE
helpviewer_keywords:
- CoInitializeEE function [.NET Framework hosting]
ms.assetid: 7e42a928-5068-4ba6-b8c3-806551a01fa8
topic_type:
- apiref
ms.openlocfilehash: 57508a2df3a49c39d25347f2a3038442c37278da
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616763"
---
# <a name="coinitializeee-function"></a>CoInitializeEE 関数
共通言語ランタイムの実行エンジンが確実にプロセスに読み込まれるようにします。 この関数は .NET Framework 4 では非推奨とされます。 代わりに[ICLRRuntimeHost:: Start](iclrruntimehost-start-method.md)メソッドを使用してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CoInitializeEE (  
   [in] DWORD fFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `fFlags`  
 から[Coinitiee](../metadata/coinitiee-enumeration.md)列挙定数の1つ。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、Winerror.h で定義されている標準 COM エラーコードと、次の表の値を返します。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|S_OK|実行エンジンが正常に読み込まれました。|  
|S_FALSE|実行エンジンは既に読み込まれています。|  
|E_FAIL|実行エンジンを読み込めませんでした。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、まだ読み込まれていない場合、実行エンジンを読み込みます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Cor  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [メタデータ グローバル静的関数](../metadata/metadata-global-static-functions.md)
