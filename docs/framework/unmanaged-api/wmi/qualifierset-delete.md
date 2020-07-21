---
title: QualifierSet_Delete関数 (アンマネージ API リファレンス)
description: QualifierSet_Delete関数は、名前によって修飾子を削除します。
ms.date: 11/06/2017
api_name:
- QualifierSet_Delete
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Delete
helpviewer_keywords:
- QualifierSet_Delete function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 0d2a02ba9d89ba16e776bb73563eaebf8a92f1fd
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174902"
---
# <a name="qualifierset_delete-function"></a>QualifierSet_Delete 関数
名前によって指定した修飾子が削除されます。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT QualifierSet_Delete (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr,
   [in] LPCWSTR              wszName
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset)へのポインター。

`wszName`[in]削除する修飾子の名前。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | `wszName` パラメーターが正しくありません。 |
|`WBEM_E_INVALID_OPERATION` | 0x80041016 | この修飾子を削除することは無効です。 |
|`WBEM_E_NOT_FOUND` | 0x80041002 | 指定された修飾子が見つかりませんでした。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
| `WBEM_S_RESET_TO_DEFAULT` | 0x40002 | ローカルオーバーライドが削除され、親オブジェクトの元の修飾子がスコープを再開しました。 |

## <a name="remarks"></a>解説

この関数は[、:D メソッド](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-delete)の呼び出しをラップします。

修飾子の伝達規則により、特定の修飾子が別のオブジェクトから継承され、現在のクラスまたはインスタンスでオーバーライドされただけである可能性があります。 この場合、メソッドは`QualifierSet_Delete`修飾子を元の継承値にリセットします。 この場合の関数は、状態コード`WBEM_S_RESET_TO_DEFAULT`を返します。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
