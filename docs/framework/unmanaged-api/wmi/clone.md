---
title: クローン関数 (アンマネージ API リファレンス)
description: Clone 関数は、現在のオブジェクトの完全なクローンである新しいオブジェクトを返します。
ms.date: 11/06/2017
api_name:
- Clone
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Clone
helpviewer_keywords:
- Clone function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: cb4951a1f289417482bfa1287028cc66349a5938
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176852"
---
# <a name="clone-function"></a>Clone 関数
現在のオブジェクトの完全な複製である新しいオブジェクトが返されます。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Clone (
   [in] int                  vFunc,
   [in] IWbemClassObject*    ptr,
   [out] IWbemClassObject**  ppCopy
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`ppCopy`  
[アウト]の完全な孤独である新しいオブジェクト`ptr`。 この引数は、`null`現在のオブジェクトのコピーを受け取った場合は使用できません。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 一般的なエラーが発生しました。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `null`はパラメータとして指定されており、この使用法では有効ではありません。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足でオブジェクトのクローンを作成できません。 |
| `WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出しをラップ[します](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-clone)。

複製されたオブジェクトは、参照カウントが 1 の COM オブジェクトです。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
