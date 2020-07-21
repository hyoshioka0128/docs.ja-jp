---
title: メソッドの削除関数 (アンマネージ API リファレンス)
description: DeleteMethod 関数は、指定されたメソッドを CIM クラス定義から削除します。
ms.date: 11/06/2017
api_name:
- DeleteMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- DeleteMethod
helpviewer_keywords:
- DeleteMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 4059555d74c0b0f151332ddcf9faedecf238e795
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174993"
---
# <a name="deletemethod-function"></a>DeleteMethod 関数
CIM クラス定義から指定したメソッドを削除します。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Delete (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszName
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`wszName`  
[in]クラス テーブルから削除するメソッドの名前。 `wszName`は有効な`LPCWSTR`.

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_E_NOT_FOUND` | 0x80041002 | 指定されたメソッドは存在しません。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 操作を完了させるための十分なメモリがありません。 |
| `WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |

## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[:Dを](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-deletemethod)ラップします。

メソッドの削除は、CIM インスタンスを指す[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)ポインターではサポートされていません。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
