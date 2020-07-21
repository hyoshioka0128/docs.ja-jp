---
title: 次のメソッド関数 (アンマネージ API リファレンス)
description: NextMethod 関数は、列挙型の次のメソッドを取得します。
ms.date: 11/06/2017
api_name:
- NextMethod
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- NextMethod
helpviewer_keywords:
- NextMethod function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 36acd6135110a8865bd8efdda628c352c01b4f26
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174928"
---
# <a name="nextmethod-function"></a>NextMethod 関数
[呼](beginmethodenumeration.md)び出しで始まる列挙体の次のメソッドを取得します。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT NextMethod (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LONG                lFlags,
   [out] BSTR*              pName,
   [out] IWbemClassObject** ppInSignature,
   [out] IWbemClassObject** ppOutSignature
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`lFlags`  
[in] 予約されています。 このパラメーターは 0 でなければなりません。

`pName`  
[アウト]呼び出しの`null`前を指すポインター。 関数が返されるときに、メソッド名を含む`BSTR`新しいアドレス。

`ppSignatureIn`  
[アウト]メソッドの`in`パラメーターを含む[IWbemClass オブジェクト](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインターを受け取るポインター。

`ppSignatureOut`  
[アウト]メソッドの`out`パラメーターを含む[IWbemClass オブジェクト](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインターを受け取るポインター。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_E_UNEXPECTED` | 0x8004101d | [`BeginEnumeration`](beginenumeration.md)関数への呼び出しはありませんでした。 |
| `WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | 列挙体にこれ以上のプロパティはありません。 |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出しをラップ[します](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod)。

呼び出し元は[、呼](beginmethodenumeration.md)び出すことによって列挙シーケンスを開始します。 `WBEM_S_NO_MORE_DATA` 必要に応じて、呼び出し元は[、呼](endmethodenumeration.md)び出しによってシーケンスを終了します。 呼び出し元は、いつでも呼び出すことによって、列挙[を](endmethodenumeration.md)早期に終了できます。

## <a name="example"></a>例

C++ の例については、メソッドを参照[してください](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-nextmethod)。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
