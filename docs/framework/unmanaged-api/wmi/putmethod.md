---
title: プットメソッド関数 (アンマネージ API リファレンス)
description: メソッドを作成する関数です。
ms.date: 11/06/2017
api_name:
- PutMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- PutMethod
helpviewer_keywords:
- PutMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 93347b7290211b5d62829604678261fdf4da1ec3
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174915"
---
# <a name="putmethod-function"></a>PutMethod 関数
メソッドが作成されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp  
HRESULT PutMethod (
   [in] int                vFunc,
   [in] IWbemClassObject*  ptr,
   [in] LPCWSTR            wszName,
   [in] LONG               lFlags,
   [in] IWbemClassObject*  pInSignature,
   [in] IWbemClassObject*  pOutSignature
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`wszName`  
[in]作成するメソッドの名前。

`lFlags`  
[in] 予約されています。 このパラメーターは 0 でなければなりません。

`pSignatureIn`  
[in]メソッドのパラメーターを格納している[__Parametersシステム クラス](/windows/desktop/WmiSdk/--parameters)の`in`コピーへのポインター。 このパラメータは、 に`null`設定されている場合は無視されます。  

`pSignatureOut`  
[in] メソッドのパラメーターを格納している[__Parametersシステム クラス](/windows/desktop/WmiSdk/--parameters)の`out`コピーへのポインター。 このパラメータは、 に`null`設定されている場合は無視されます。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 1 つ以上のパラメーターが無効です。 |
| `WBEM_E_INVALID_DUPLICATE_PARAMETER` | 0x80041043 | pInSignature オブジェクトと`[in, out]` *pOutSignature* *pOutSignature*オブジェクトの両方で指定されたメソッド パラメーターには、異なる修飾子があります。
| `WBEM_E_MISSING_PARAMETER_ID` | 0x80041036 | メソッド パラメータに**ID**修飾子の指定がありません。 |
| `WBEM_E_NONCONSECUTIVE_PARAMETER_IDS` | 0x80041038 | メソッド パラメータに割り当てられた ID シリーズが連続していないか、0 から始まらない。 |
| `WBEM_E_PARAMETER_ID_ON_RETVAL` | 0x80041039 | メソッドの戻り値には**ID**修飾子があります。 |
| `WBEM_E_PROPAGATED_METHOD` | 0x80041034 | 親クラスから既存のメソッド名を再利用しようとしましたが、シグネチャが一致しませんでした。 |
| `WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。 |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[:Pをラップします](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-putmethod)。

このメソッド呼び出しは`ptr`、CIM クラス定義の場合にのみサポートされます。 メソッド操作は、CIM インスタンスを指す[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)ポインターからは使用できません。

ユーザーは、アンダースコアで始まる名前または末尾に名前を付けてメソッドを作成することはできません。 これは、システム クラスとプロパティ用に予約されています。

メソッドの場合、`in`および`out`パラメーターは[IWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)オブジェクトのプロパティとして記述されます。

パラメーター`[in/out]`は、`pInSignature`パラメーター`pOutSignature`が指すオブジェクトと の両方に同じプロパティを追加することで定義できます。 この場合、プロパティは同じ**ID**修飾子の値を共有します。

[__Parameters](/windows/desktop/WmiSdk/--parameters)クラス オブジェクトの各プロパティには`ReturnValue`**、ID**修飾子 (パラメーターが出現する順序を識別する 0 から始まる数値) が必要です。 2 つのパラメーターに同じ**ID**値を**ID**指定することはできません。 いずれかの条件が発生した場合、`PutMethod`関数は`WBEM_E_NONCONSECUTIVE_PARAMETER_IDS`を返します。

## <a name="example"></a>例

例については、メソッド[:P](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-putmethod)を参照してください。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
