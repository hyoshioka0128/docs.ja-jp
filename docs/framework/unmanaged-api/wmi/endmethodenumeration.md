---
title: メソッド列挙関数 (アンマネージ API リファレンス)
description: 関数は、メソッド列挙体のシーケンスを終了します。
ms.date: 11/06/2017
api_name:
- EndMethodEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- EndMethodEnumeration
helpviewer_keywords:
- EndMethodEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 63667d0668f905ded2aedd961be0d1831faf838c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79175006"
---
# <a name="endmethodenumeration-function"></a>EndMethodEnumeration 関数
関数の呼び出しで開始される列挙シーケンス[を](beginmethodenumeration.md)終了します。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EndMethodEnumeration (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_UNEXPECTED` | 0x8004101d | An internal error occurred. |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[をラップします](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-endmethodenumeration)。

呼び出し元は[、BeginMethodEnumeration 関数](beginmethodenumeration.md)を使用して列挙シーケンスを開始し、メソッドが`WBEM_S_NO_MORE_DATA`返されるまで[NextMethod 関数](nextmethod.md )を呼び出します。 呼び出し元はオプションで、`EndMethodEnumeration`を呼び出してシーケンスを終了します。 呼び出し元は、いつでも呼`EndMethodEnumeration`び出すことによって、列挙を早期に終了できます。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
