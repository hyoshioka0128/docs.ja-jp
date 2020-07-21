---
title: QualifierSet_Next関数 (アンマネージ API リファレンス)
description: QualifierSet_Next関数は、列挙体の次の修飾子を取得します。
ms.date: 11/06/2017
api_name:
- QualifierSet_Next
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Next
helpviewer_keywords:
- QualifierSet_Next function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: d3702426bc409d601ccfc6b7a8e93e8d9729c64e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174876"
---
# <a name="qualifierset_next-function"></a>QualifierSet_Next 関数
[QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md) 関数の呼び出しによって開始された列挙型内の次の修飾子が返されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT QualifierSet_Next (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LONG                 lFlags,
   [out] BSTR*               pstrName,
   [out] VARIANT*            pVal,
   [out] LONG*               plFlavor
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`[in]このパラメーターは使用されません。

`ptr`[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset)へのポインター。

`lFlags`[in]予約。 このパラメーターは 0 でなければなりません。

`pstrName`[アウト]修飾子の名前。 の`null`場合、このパラメータは無視されます。それ以外`pstrName`の場合は、有効`BSTR`なメモリ リークが発生することを指す必要があります。 null でない場合、関数は戻るときに`BSTR``WBEM_S_NO_ERROR`常に新しいを割り当てます。

`pVal`[アウト]成功した場合は、修飾子の値。 関数が失敗した場合、`VARIANT`指すが`pVal`変更されません。 このパラメーターが`null`の場合、パラメーターは無視されます。

`plFlavor`[アウト]修飾子のフレーバーを受け取る LONG へのポインター。 フレーバー情報が必要ない場合、このパラメーターは`null`.

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | パラメーターが無効です。 |
|`WBEM_E_UNEXPECTED` | 0x8004101d | 呼び出し元は[QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md)を呼び出しませんでした。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足で新しい列挙を開始できません。 |
| `WBEM_S_NO_MORE_DATA` | 0x40005 | 列挙体に修飾子が残っていません。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は[、IWbemQualifierSet::Next](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-next)メソッドへの呼び出しをラップします。

関数が`QualifierSet_Next`戻`WBEM_S_NO_MORE_DATA`るまで、関数を繰り返し呼び出してすべての修飾子を列挙します。 列挙を早期に終了するには[、QualifierSet_EndEnumeration](qualifierset-endenumeration.md)関数を呼び出します。

列挙時に返される修飾子の順序は未定義です。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
