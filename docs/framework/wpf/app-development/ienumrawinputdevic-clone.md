---
title: IEnumRAWINPUTDEVIC:Clone
ms.date: 03/30/2017
helpviewer_keywords:
- Clone method [WPF]
ms.assetid: 2a6a1900-aa55-45fa-9382-241d569a2dc4
ms.openlocfilehash: cd634b4d4a88d83d425b787ed8493f9aa2504988
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053417"
---
# <a name="ienumrawinputdevicclone"></a>IEnumRAWINPUTDEVIC:Clone
同じリストを反復処理するため、現在の列挙子と同じ状態の別の未加工入力デバイスの列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Clone( [out] IEnumRAWINPUTDEVICE **ppenum);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppenum`  
  
 [out] [IEnumRAWINPUTDEVICE](ienumrawinputdevice.md) インターフェイス ポインターを受け取る出力変数のアドレス。 メソッドが失敗した場合、この出力変数の値は未定義になります。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 HRESULT:このメソッドでは、標準の戻り値 E_INVALIDARG、E_OUTOFMEMORY、E_UNEXPECTED がサポートされています。  
  
## <a name="remarks"></a>Remarks  
 このメソッドを使用すると、列挙シーケンス内のポイントを記録でき、後でそのポイントに戻ることができます。 呼び出し元では、最初の列挙子とは別に、この新しい列挙子を解放する必要があります。
