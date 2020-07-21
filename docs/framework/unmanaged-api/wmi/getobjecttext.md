---
title: 関数を取得します (アンマネージ API リファレンス)
description: 関数は、MOF 構文でオブジェクトのテキストレンダリングを返します。
ms.date: 11/06/2017
api_name:
- GetObjectText
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetObjectText
helpviewer_keywords:
- GetObjectText function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 6881125760e0f1dc38e6b01917d5829edc95e3ca
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176787"
---
# <a name="getobjecttext-function"></a>GetObjectText 関数
マネージ オブジェクト 形式 (MOF) 構文でオブジェクトのテキストレンダリングを返します。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetObjectText (
   [in] int                vFunc,
   [in] IWbemClassObject*   ptr,
   [in] LONG                lFlags,
   [out] BSTR*              pstrObjectText
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`lFlags`  
[in]通常 0. (`WBEM_FLAG_NO_FLAVORS`または 0x1) を指定すると、修飾子は伝搬情報やフレーバー情報なしで組み込まれます。

`pstrObjectText`[アウト]`null`オン エントリへのポインター。 戻り値の場合、オブジェクト`BSTR`の MOF 構文レンダリングを含む、新しく割り当てられたもの。  

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 一般的なエラーが発生しました。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | パラメーターが無効です。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足のため、操作を完了できません。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[を](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getobjecttext)ラップします。

返される MOF テキストには、オブジェクトに関するすべての情報が含まれているわけではありませんが、MOF コンパイラが元のオブジェクトを再作成するのに十分な情報だけが含まれています。 たとえば、伝達された修飾子や親クラスのプロパティは含まれません。

メソッドのパラメータのテキストを再構築するには、次のアルゴリズムを使用します。

1. パラメーターは、ID 値の順序で再シーケンスされます。
1. として指定され`[in]`、1`[out]`つのパラメーターに結合されるパラメーター。

`pstrObjectText`関数が呼び出されるとき`null`のポインタでなければなりません。ポインターの割り当て解除は行わないため、メソッド呼び出しの前に有効な文字列を指してはいけません。

## <a name="requirements"></a>必要条件  
**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
