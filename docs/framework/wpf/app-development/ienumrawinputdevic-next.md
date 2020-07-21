---
title: IEnumRAWINPUTDEVIC:Next
ms.date: 03/30/2017
helpviewer_keywords:
- Next method [WPF]
ms.assetid: 3698b44d-510e-4d18-b32b-85f17188ee26
ms.openlocfilehash: c7450a9ababa9cf3cb02d572f5ed84f0791d74e4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053399"
---
# <a name="ienumrawinputdevicnext"></a>IEnumRAWINPUTDEVIC:Next
列挙子の一覧に含まれる次の `celt` 個の [RAWINPUTDEVICE](/windows/desktop/api/winuser/ns-winuser-rawinputdevice) 構造体を列挙し、それを `pceltFetched` で列挙された要素の実際の数とともに `rgelt` で返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next(  
      [in] ULONG celt,  
      [out, size_is(celt), length_is(*pceltFetched)] RAWINPUTDEVICE *rgelt,  
      [out] ULONG *pceltFetched);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
  
 [in] `rgelt` で返される [RAWINPUTDEVICE](/windows/desktop/api/winuser/ns-winuser-rawinputdevice) 構造体の数。  
  
 `rgelt`  
  
 [out] 列挙された RAWINPUTDEVICE 構造体を受け取る size celt (またはそれ以上) の配列。  
  
 `pceltFetched`  
  
 [out] `rgelt` に実際に指定された要素の数へのポインター。 `NULL` が 1 の場合、呼び出し元は `rgelt` に渡すことができます。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 HRESULT:指定された要素の数が `celt` の場合は S_OK。それ以外の場合は S_FALSE。
