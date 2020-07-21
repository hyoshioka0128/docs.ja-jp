---
title: 継承関数 (アンマネージ API リファレンス)
description: InheritsFrom 関数は、クラスまたはインスタンスが特定の親クラスから派生するかどうかを決定します。
ms.date: 11/06/2017
api_name:
- InheritsFrom
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- InheritsFrom
helpviewer_keywords:
- InheritsFrom function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: c735c01c45beda8a1ba988a5c580e6b04ae46312
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174941"
---
# <a name="inheritsfrom-function"></a>InheritsFrom 関数
指定した親クラスから現在のクラスまたはインスタンスが派生しているかどうかが判定されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp
HRESULT InheritsFrom (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszAncestor
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`wszAncestor`  
[in]クラスの名前。 `wszAncestor`有効な`LPCWSTR`を指す必要があります。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_S_NO_ERROR` | 0 | 現在のオブジェクトは`wszAncestor`から継承されます。  |
| `WBEM_S_FALSE` | 1 | 現在のオブジェクトは`wszAncestor`から継承しません。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | `wszAncestor` は `null` です。 |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[を](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-inheritsfrom)ラップします。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
