---
title: 列挙関数 (アンマネージ API リファレンス)
description: 列挙子を列挙の先頭にリセットします。
ms.date: 11/06/2017
api_name:
- BeginEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BeginEnumeration
helpviewer_keywords:
- BeginEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: eac23916bd78ec3970a87566e2d2f4d79b379824
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176878"
---
# <a name="beginenumeration-function"></a>BeginEnumeration 関数
列挙子を列挙の先頭にリセットします。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT BeginEnumeration (
   [in] int               vFunc,
   [in] IWbemClassObject* ptr,
   [in] LONG              lEnumFlags
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`\
[in]このパラメーターは使用されません。

`ptr`\
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`lEnumFlags`\
[in]列挙体に含まれるプロパティを制御する[「解説」](#remarks)セクションで説明されているフラグまたは値のビットごとの組み合わせ。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | フラグの組み合`lEnumFlags`わせが無効か、無効な引数が指定されました。 |
|`WBEM_E_UNEXPECTED` | 0x8004101d | への 2`BeginEnumeration`回目の呼び出しは、間[`EndEnumeration`](endenumeration.md)に呼び出されることなく行われました。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足で新しい列挙を開始できません。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、[メソッド](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)の呼び出しをラップします。

`lEnumFlags`引数として渡すことができるフラグは *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。  各グループの 1 つのフラグを、他のグループの任意のフラグと組み合わせることができます。 ただし、同じグループのフラグは相互に排他的です。

**グループ 1**

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | 0x4 | キーのみを構成するプロパティを含めます。 |
|`WBEM_FLAG_REFS_ONLY` | 0x8 | オブジェクト参照だけのプロパティを含めます。 |

**グループ 2**

常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_FLAG_SYSTEM_ONLY` | 0x30 | 列挙をシステム プロパティのみに制限します。 |
|`WBEM_FLAG_NONSYSTEM_ONLY` | 0x40 | ローカル プロパティと反映プロパティを含めますが、列挙体からシステム プロパティを除外します。 |

クラスの場合:

常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_FLAG_CLASS_OVERRIDES_ONLY` | 0x100 | 列挙型をクラス定義でオーバーライドされたプロパティに制限します。 |
|`WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` | 0x100 | 列挙型を、現在のクラス定義でオーバーライドされたプロパティと、クラスで定義された新しいプロパティに制限します。 |
| `WBEM_MASK_CLASS_CONDITION` | 0x300 | いずれかの`WBEM_FLAG_CLASS_OVERRIDES_ONLY`値が設定されているか、または`WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES`設定されているかを確認する`lEnumFlags`値に適用するマスク (フラグではなく) です。 |
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 列挙型を、クラス自体で定義または変更されたプロパティに制限します。 |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 列挙型を、基本クラスから継承されるプロパティに制限します。 |

インスタンスの場合:

常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | 0x10 | 列挙型を、クラス自体で定義または変更されたプロパティに制限します。 |
| `WBEM_FLAG_PROPAGATED_ONLY` |  0x20 | 列挙型を、基本クラスから継承されるプロパティに制限します。 |

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
