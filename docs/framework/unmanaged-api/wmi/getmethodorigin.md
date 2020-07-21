---
title: 関数 (アンマネージ API リファレンス)
description: 関数は、メソッドが宣言されているクラスを決定します。
ms.date: 11/06/2017
api_name:
- GetMethodOrigin
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetMethodOrigin
helpviewer_keywords:
- GetMethodOrigin function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 5b4609b6649be875aea7dfcf52ba36b1e98ab7bc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176800"
---
# <a name="getmethodorigin-function"></a>GetMethodOrigin 関数
メソッドを宣言しているクラスが特定されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMethodOrigin (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LPCWSTR             wszMethodName,
   [out] BSTR*              pstrClassName
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`wszMethodName`  
[in]所有クラスが要求されているオブジェクトのメソッドの名前。

`pstrClassName`  
[アウト]メソッドを所有するクラスの名前を受け取ります。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_NOT_FOUND` | 0x80041002 | 指定されたメソッドが見つかりませんでした。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 1 つ以上のパラメーターが無効です。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[を](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getmethod)ラップします。

クラスは 1 つ以上の基本クラスからメソッドを継承できるため、開発者は、特定のメソッドが定義されているクラスを決定する必要があります。

この`pstrClassName`パラメーターはパラメーターであるため、関数が`BSTR`呼び出される前にパラメーターが有効`out`であることを指してはなりません。このポインターは、関数が戻った後に割り当て解除されません。

## <a name="requirements"></a>必要条件  
**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
