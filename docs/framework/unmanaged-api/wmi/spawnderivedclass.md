---
title: 関数 (アンマネージ API リファレンス)
description: 関数は、オブジェクトから派生する新しいオブジェクトを作成します。
ms.date: 11/06/2017
api_name:
- SpawnDerivedClass
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SpawnDerivedClass
helpviewer_keywords:
- SpawnDerivedClass function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: e9784f8a024c788823dc702794b2b86eea1827bb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174850"
---
# <a name="spawnderivedclass-function"></a>SpawnDerivedClass 関数
指定したオブジェクトから新たに派生するクラス オブジェクトが作成されます。
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SpawnDerivedClass (
   [in] int                  vFunc,
   [in] IWbemClassObject*    ptr,
   [in] LONG                 lFlags,
   [out] IWbemClassObject**  ppNewClass);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`lFlags`  
[in] 予約されています。 このパラメーターは 0 でなければなりません。

`ppNewClass`  
[アウト]新しいクラス定義オブジェクトへのポインターを受け取ります。 エラーが発生した場合、新しいオブジェクトは返されず、`ppNewClass`変更されません。 その値を指定`null`することはできません。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 一般的なエラーが発生しました。 |
| `WBEM_E_INVALID_OPERATION` | 0x80041016 | インスタンスからクラスを生成するなどの無効な操作が要求されました。 |
| `WBEM_E_INCOMPLETE_CLASS` | ソース クラスが完全に定義されていないか、Windows の管理に登録されていないので、新しい派生クラスは許可されていません。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足のため、操作を完了できません。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `ppNewClass` は `null` です。 |
| `WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[を](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-clone)ラップします。

`ptr`は、スポーンされたオブジェクトの親クラスとなるクラス定義である必要があります。 返されたオブジェクトは、現在のオブジェクトのサブクラスになります。

返される新しいオブジェクト`ppNewClass`は、自動的に現在のオブジェクトのサブクラスになります。 この動作はオーバーライドできません。 サブクラス (派生クラス) を作成できるメソッドは他にありません。

## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
