---
title: 関数 (アンマネージ API リファレンス)
description: 関数は、プロパティにバイトを書き込みます。
ms.date: 11/06/2017
api_name:
- WritePropertyValue
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- WritePropertyValue
helpviewer_keywords:
- WritePropertyValue function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 4a950beef2e9bf8c0230d6a38008d75f89373410
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174837"
---
# <a name="writepropertyvalue-function"></a>WritePropertyValue 関数
指定したバイト数が、プロパティ ハンドルによって識別されるプロパティに書き込まれます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp  
HRESULT WritePropertyValue (
   [in] int                  vFunc,
   [in] IWbemObjectAccess*   ptr,
   [in] long                 lHandle,
   [in] long                 lNumBytes,
   [in] byte*                aData
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemobjectaccess)へのポインター。

`lHandle`  
[in]このプロパティを識別するハンドルを格納する整数。 ハンドルは、[関数](getpropertyhandle.md)を呼び出すことによって取得できます。

`lNumBytes`  
[in]プロパティに書き込まれるバイト数。 詳細[については、「解説」](#remarks)を参照してください。

`pHandle`[アウト]データを格納するバイト配列へのポインター。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | パラメーターが無効です。 |
|`WBEM_E_TYPE_MISMATCH` | 0x80041005 | 型の不一致が発生しました。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[を](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemobjectaccess-writepropertyvalue)ラップします。

この関数は、文字列と、その他の非`DWORD``QWORD`データまたは非データをすべて設定するために使用します。

文字列以外のプロパティ値の`lNumBytes`場合は、指定したプロパティ型の正しいデータ サイズを指定する必要があります。 文字列プロパティ値の場合`lNumBytes`、指定した文字列の長さ (バイト単位) を指定し、文字列自体はバイト単位で偶数の長さでなければならず、その後に null 終端文字が続く必要があります。

## <a name="requirements"></a>必要条件  
**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
