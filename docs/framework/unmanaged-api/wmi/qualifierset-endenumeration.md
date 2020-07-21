---
title: QualifierSet_EndEnumeration関数 (アンマネージ API リファレンス)
description: QualifierSet_EndEnumeration関数は、列挙を終了します。
ms.date: 11/06/2017
api_name:
- QualifierSet_EndEnumeration
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_EndEnumeration
helpviewer_keywords:
- QualifierSet_EndEnumeration function [.NET WMI and performance counters]
topic_type:
- Reference
ms.openlocfilehash: c606580ff2e02c5659c14b134b1a17a65651952b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176748"
---
# <a name="qualifierset_endenumeration-function"></a>QualifierSet_EndEnumeration 関数
[QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md)関数の呼び出しで始まる列挙を終了します。  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT QualifierSet_EndEnumeration (
   [in] int                  vFunc,
   [in] IWbemQualifierSet*   ptr
);
```  

## <a name="parameters"></a>パラメーター

`vFunc`  
[in]このパラメーターは使用されません。

`ptr`[in][インスタンス](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset)へのポインター。

## <a name="return-value"></a>戻り値

この関数によって返される次の値は *、WbemCli.h*ヘッダー ファイルで定義されているか、コード内で定数として定義できます。

|常時  |Value  |説明  |
|---------|---------|---------|
|`WBEM_S_NO_ERROR` | 0 | 関数呼び出しが正常に行われました。  |
  
## <a name="remarks"></a>解説

この関数は、メソッドの呼び出し[を](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-endenumeration)ラップします。

この呼び出しは推奨されますが、必須ではありません。 列挙に関連付けられたリソースをすぐに解放します。

## <a name="requirements"></a>必要条件  

**:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
**ヘッダー:** WMINet_Utils.idl  
  
**.NET Framework のバージョン:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [WMI およびパフォーマンス カウンター (アンマネージド API リファレンス)](index.md)
