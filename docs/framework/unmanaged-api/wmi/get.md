---
title: 関数の取得 (アンマネージ API リファレンス)
description: Get 関数は、指定されたプロパティ値を取得します。
ms.date: 11/06/2017
api_name:
- Get
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- Get
helpviewer_keywords:
- Get function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 67fcfb301eebfcf4ed4fdcaa5c9ddf85c47a6073
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174980"
---
# <a name="get-function"></a>Get 関数

指定したプロパティ値が存在する場合は、その値を取得します。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文

```cpp
HRESULT Get (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LPCWSTR           wszName,
   [in] LONG              lFlags,
   [out] VARIANT*         pVal,
   [out] CIMTYPE*         pvtType,
   [out] LONG*            plFlavor
);
```

## <a name="parameters"></a>パラメーター

`vFunc`\
[in]このパラメーターは使用されません。

`ptr`\
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`wszName`\
[in]プロパティの名前。

`lFlags`\
[in] 予約されています。 このパラメーターは 0 でなければなりません。

`pVal`\
[アウト]関数が正常に返された場合は、プロパティの値`wszName`が格納されます。 引数`pval`には、修飾子の正しい型と値が割り当てられます。

`pvtType`\
[アウト]関数が正常に返された場合は、プロパティの型を示す[CIM 型の定数](/windows/win32/api/wbemcli/ne-wbemcli-cimtype_enumeration)が含まれます。 その値も. `null`

`plFlavor`\
[アウト]関数が正常に返された場合は、プロパティの起点に関する情報を受け取ります。 この値は`null`*、WbemCli.h*ヘッダー ファイルで定義されている次のWBEM_FLAVOR_TYPE定数のいずれかです。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_FLAVOR_ORIGIN_SYSTEM` | 0x40 | プロパティは、標準のシステム プロパティです。 |
| `WBEM_FLAVOR_ORIGIN_PROPAGATED` | 0x20 | クラスの場合: プロパティは親クラスから継承されます。 <br> インスタンスの場合: 親クラスから継承されたプロパティは、インスタンスによって変更されていません。  |
| `WBEM_FLAVOR_ORIGIN_LOCAL` | 0 | クラスの場合: プロパティは派生クラスに属します。 <br> インスタンスの場合: プロパティはインスタンスによって変更されます。つまり、値が指定されたか、修飾子が追加または変更された場合。 |

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 一般的なエラーが発生しました。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | 1 つ以上のパラメーターが無効です。 |
|`WBEM_E_NOT_FOUND` | 0x80041002 | 指定されたプロパティが見つかりませんでした。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足のため、操作を完了できません。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |

## <a name="remarks"></a>解説

この関数は、[メソッド](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-get)の呼び出しをラップします。

この`Get`関数はシステム プロパティを返すこともできます。

引数`pVal`には、修飾子と COM [VariantInit](https://docs.microsoft.com/previous-versions/windows/desktop/api/oleauto/nf-oleauto-variantinit)関数に対して正しい型と値が割り当てられます。

## <a name="requirements"></a>必要条件

 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。

 **ヘッダー:** WMINet_Utils.idl

 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
