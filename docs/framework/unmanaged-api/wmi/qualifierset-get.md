---
title: QualifierSet_Get関数 (アンマネージ API リファレンス)
description: QualifierSet_Get関数は、名前付き修飾子を取得します。
ms.date: 11/06/2017
api_name:
- QualifierSet_Get
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Get
helpviewer_keywords:
- QualifierSet_Get function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 2f4e2d4518e01f3415b8f17ce5778dd98b2a45c3
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174889"
---
# <a name="qualifierset_get-function"></a>QualifierSet_Get 関数
指定した名前付き修飾子が取得されます。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT QualifierSet_Get (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LPCWSTR              wszName,
   [in] LONG                 lFlags,
   [out] VARIANT*            pVal,
   [out] LONG*               plFlavor
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`[in]このパラメーターは使用されません。

`ptr`[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset)へのポインター。

`wszName`[in]値が要求された修飾子の名前。

`lFlags`[in]予約。 このパラメーターは 0 でなければなりません。

`pVal`[アウト]成功した場合は、修飾子の正しい型と値。 関数が失敗した場合、`VARIANT`指すが`pVal`変更されません。 このパラメーターが`null`の場合、パラメーターは無視されます。

`plFlavor`[アウト]要求された修飾子の修飾子フレーバー ビットを受け取る LONG へのポインター。 フレーバー情報が必要ない場合、このパラメーターは`null`.

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | パラメーターが無効です。 |
|`WBEM_E_NOT_FOUND` | 0x80041002 | 指定された修飾子が存在しません。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は[、IWbemQualifierSet::Get](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-get)メソッドへの呼び出しをラップします。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
