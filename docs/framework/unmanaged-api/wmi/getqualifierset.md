---
title: 取得修飾子セット関数 (アンマネージ API リファレンス)
description: 関数は、クラスまたはインスタンスの修飾子セットを取得します。
ms.date: 11/06/2017
api_name:
- GetQualifierSet
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- GetQualifierSet
helpviewer_keywords:
- GetQualifierSet function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: 368f0a13871bd48780fa30b370d37157d2724bb8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176774"
---
# <a name="getqualifierset-function"></a>GetQualifierSet 関数
クラス インスタンスまたはクラス定義で設定された修飾子が取得されます。

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetQualifierSet (
   [in] int                 vFunc,
   [in] IWbemClassObject*   ptr,
   [out] IWbemQualifierSet  **ppQualSet
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`  
[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemclassobject)へのポインター。

`ppQualSet`  
[アウト]クラス オブジェクトの修飾子へのアクセスを許可するインターフェイス ポインターを受け取ります。 `ppQualSet` として `null` を使用することはできません。 エラーが発生した場合、新しいオブジェクトは返されず、ポインターは変更されません。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_E_FAILED` | 0x80041001 | 一般的なエラーが発生しました。 |
|`WBEM_E_NOT_FOUND` | 0x80041002 | 指定されたメソッドは存在しません。 |
|`WBEM_E_OUT_OF_MEMORY` | 0x80041006 | メモリ不足のため、操作を完了できません。 |
|`WBEM_E_INVALID_PARAMETER` | 0x80041008 | パラメータは`null`です。 |
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[を](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemclassobject-getqualifierset)ラップします。

[IWbemQualifierSet ポインター](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset)を使用すると、呼び出し元がこれらの修飾子を追加、編集、または削除できます。 このような追加、編集、または削除された修飾子は、インスタンスまたはクラス定義全体に適用されます。

## <a name="requirements"></a>必要条件  
**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** WMINet_Utils.idl  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
