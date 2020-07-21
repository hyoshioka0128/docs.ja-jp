---
title: 関数 (アンマネージ API リファレンス)
description: 関数は、クラスの新しいインスタンスを作成します。
ms.date: 11/06/2017
api_name:
- SpawnInstance
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SpawnInstance
helpviewer_keywords:
- SpawnInstance function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: a15eb8123c1ee807444bdb4c6fe71cdccc08f434
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176722"
---
# <a name="spawninstance-function"></a>SpawnInstance 関数
クラスの新しいインスタンスが作成されます。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SpawnInstance (
   [in] int                  vFunc,
   [in] IWbemClassObject*    ptr,
   [in] LONG                 lFlags,
   [out] IWbemClassObject**  ppNewInstance);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`lFlags`  
[in] 予約されています。 このパラメーターは 0 でなければなりません。

`ppNewInstance`  
[アウト]クラスの新しいインスタンスへのポインターを受け取ります。 エラーが発生した場合、新しいオブジェクトは返されず、`ppNewInstance`変更されません。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_E_INCOMPLETE_CLASS` | 0x80041020 | `ptr`は有効なクラス定義ではないため、新しいインスタンスを生成できません。 不完全であるか、[または PutClassWmi](putclasswmi.md)を呼び出して Windows 管理に登録されていません。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足のため、操作を完了できません。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `ppNewClass` は `null` です。 |
| `WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[を](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-spawninstance)ラップします。

`ptr`は、Windows 管理から取得したクラス定義である必要があります。 (インスタンスからのインスタンスの生成はサポートされていますが、返されるインスタンスは空です)。次に、このクラス定義を使用して新しいインスタンスを作成します。 インスタンスを Windows 管理に書き込む場合は[、PutInstanceWmi](putinstancewmi.md)関数の呼び出しが必要です。

返される新しいオブジェクト`ppNewClass`は、自動的に現在のオブジェクトのサブクラスになります。 この動作はオーバーライドできません。 サブクラス (派生クラス) を作成できるメソッドは他にありません。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
