---
title: メソッド列挙関数 (アンマネージ API リファレンス)
description: 関数は、オブジェクトのメソッドの列挙体を開始します。
ms.date: 11/06/2017
api_name:
- BeginMethodEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BeginMethodEnumeration
helpviewer_keywords:
- BeginMethodEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 876f5810fffab7fa98cd4d46715e13569ab95f6c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79175045"
---
# <a name="beginmethodenumeration-function"></a>BeginMethodEnumeration 関数
オブジェクトに対して使用できるメソッドの列挙を開始します。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp
HRESULT BeginMethodEnumeration (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              lEnumFlags
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`lEnumFlags`  
[in]すべてのメソッドに対してゼロ (0) を指定するか、列挙のスコープを指定するフラグを指定します。 次のフラグは *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 列挙型を、クラス自体で定義されているメソッドに制限します。 |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 列挙型を、基本クラスから継承されるプロパティに制限します。 |

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | `lEnnumFlags`はゼロ以外であり、指定されたフラグの 1 つではありません。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[をラップします](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-beginmethodenumeration)。

このメソッド呼び出しは、現在のオブジェクトがクラス定義の場合にのみサポートされます。 メソッド操作は、インスタンスを指す[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)ポインターからは使用できません。 メソッドが列挙される順序は、指定されたインスタンスの[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)に対して不変であることが保証されます。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
