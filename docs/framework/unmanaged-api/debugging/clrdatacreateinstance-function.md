---
title: CLRDataCreateInstance 関数
ms.date: 03/30/2017
api_name:
- CLRDataCreateInstance
api_location:
- mscordbi.dll
- mscordacwks.dll
api_type:
- COM
f1_keywords:
- CLRDataCreateInstance
helpviewer_keywords:
- CLRDataCreateInstance function [.NET Framework debugging]
ms.assetid: 440bad90-5a88-45e7-9157-4596801d8d19
topic_type:
- apiref
ms.openlocfilehash: c24963a6e56adfb9f763c6521027744db82cc357
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179363"
---
# <a name="clrdatacreateinstance-function"></a>CLRDataCreateInstance 関数
指定したターゲット項目のインターフェイス オブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CLRDataCreateInstance (  
    [in]  REFIID           iid,
    [in]  ICLRDataTarget  *target,
    [out] void           **iface  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `iid`  
 [in]インスタンス化されるインターフェイスの識別子。  
  
 `target`  
 [in]インターフェイス オブジェクトを作成する対象の項目を表す、ユーザーが実装する[ICLRDataTarget](iclrdatatarget-interface.md)オブジェクトへのポインター。  
  
 `iface`  
 [アウト]返されたインターフェイス オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 オブジェクト`ICLRDataTarget`は、デバッグ アプリケーションのライターによって実装されます。 実装は、表されるターゲット項目の型によって異なります。 ターゲット項目は、プロセス、メモリ ダンプ、リモート コンピューターなどです。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** を使用します。  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグ グローバル静的関数](debugging-global-static-functions.md)
