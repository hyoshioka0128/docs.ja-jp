---
title: GetNames 関数 (アンマネージ API リファレンス)
description: GetNames 関数は、オブジェクトのプロパティの名前を取得します。
ms.date: 11/06/2017
api_name:
- GetNames
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetNames
helpviewer_keywords:
- GetNames function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 449f0ce9c291d4bbcad4947214e56ff46f55beed
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174954"
---
# <a name="getnames-function"></a>GetNames 関数
オブジェクトのプロパティの名前の一部またはすべてが取得されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetNames (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LPCWSTR             wszQualifierName,
   [in] LONG                lFlags,
   [in] VARIANT*            pQualifierValue,
   [out] SAFEARRAY (BSTR)** pstrNames
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`wszQualifierName`  
[in]フィルターの一部として`LPCWSTR`動作する修飾子名を指定する有効なポインター。 詳細については、「[解説」](#remarks)を参照してください。 このパラメーターは、`null` に設定できます。

`lFlags`  
[in]ビット フィールドの組み合わせ。 詳細については、「[解説」](#remarks)を参照してください。

`pQualifierValue`[in]フィルター値に初期化された`VARIANT`有効な構造体へのポインター。 このパラメーターは、`null` に設定できます。

`pstrNames`  
[アウト]プロパティ`SAFEARRAY`名を含む構造体。 エントリ時には、このパラメーターは常に`null`へのポインターである必要があります。 詳細[については、「解説」](#remarks)を参照してください。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 一般的なエラーが発生しました。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 1 つ以上のパラメーターが無効であるか、またはフラグとパラメーターの正しくない組み合わせが指定されています。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足のため、操作を完了できません。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出しをラップ[します](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getnames)。

戻される名前は、フラグとパラメーターの組み合わせによって制御されます。 たとえば、この関数は、すべてのプロパティの名前を返したり、キー プロパティの名前のみを返したりできます。  プライマリ フィルタは`lFlags`パラメータで指定され、その他のパラメータはパラメータによって異なります。

のフラグ値`lFlags`はビットフィールドです

`lEnumFlags`引数として渡すことができるフラグは *、WbemCli.h*ヘッダー ファイルで定義されているビット フィールドか、コード内で定数として定義できます。  各グループの 1 つのフラグを、他のグループの任意のフラグと組み合わせることができます。 ただし、同じグループのフラグは相互に排他的です。

| グループ 1 フラグ |Value  |説明  |
|---------|---------|---------|
| `WBEM_FLAG_ALWAYS` | 0 | すべてのプロパティ名を返します。 `strQualifierName`が`pQualifierVal`使用されていない。 |
| `WBEM_FLAG_ONLY_IF_TRUE` | 1 | `strQualifierName`パラメーターで指定された名前の修飾子を持つプロパティのみを返します。 このフラグを使用する場合は、`strQualifierName`を指定する必要があります。 |
|`WBEM_FLAG_ONLY_IF_FALSE` | 2 |  `strQualifierName`パラメーターで指定された名前の修飾子を持たないプロパティのみを返します。 このフラグを使用する場合は、`strQualifierName`を指定する必要があります。 |
|`WBEM_FLAG_ONLY_IF_IDENTICAL` | 3 | `wszQualifierName`パラメーターで指定された名前の修飾子を持ち、`pQualifierVal`構造体で指定された値と同じ値を持つプロパティのみを返します。 このフラグを使用する場合は、 と`wszQualifierName`を両方`pQualifierValue`とも指定する必要があります。 |

| グループ 2 フラグ |Value  |説明  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | キーを定義するプロパティの名前のみを返します。 |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | オブジェクト参照であるプロパティ名のみを返します。 |

| グループ 3 フラグ |Value  |説明  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 最も派生したクラスに属するプロパティ名のみを返します。 親クラスからプロパティを除外します。 |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 親クラスに属するプロパティ名のみを返します。 |
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | システム プロパティの名前のみを返します。 |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | システムプロパティ以外の名前のみを返します。 |

関数は、 が戻`SAFEARRAY``WBEM_S_NO_ERROR`る場合は常に`pstrNames`new を割り当て、常にこの関数を指す値に設定されます。 指定したフィルターに一致するプロパティがない場合、返される配列の要素は 0 になります。 関数が`WBM_S_NO_ERROR`以外の値を返す場合、`SAFEARRAY`新しい構造体は返されません。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
