---
title: ISymUnmanagedWriter3::OpenMethod2 メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter3.OpenMethod2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter3::OpenMethod2
helpviewer_keywords:
- ISymUnmanagedWriter3::OpenMethod2 method [.NET Framework debugging]
- OpenMethod2 method [.NET Framework debugging]
ms.assetid: 025e358c-448f-4423-a2f2-57acf437c8a5
topic_type:
- apiref
ms.openlocfilehash: e88a844a7f79f14c717a5966b345588b3b3b9f81
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609418"
---
# <a name="isymunmanagedwriter3openmethod2-method"></a>ISymUnmanagedWriter3::OpenMethod2 メソッド
メソッドを開き、イメージ内の実際のセクションオフセットを提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OpenMethod2(
    [in] mdMethodDef method,  
    [in] ULONG32 isect,  
    [in] ULONG32 offset);  
```  
  
## <a name="parameters"></a>パラメーター  
 `method`  
 から開くメソッドのメタデータトークン。  
  
 `isect`  
 からイメージ内のセクションオフセット。  
  
 `offset`  
 からイメージ内のオフセット。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter3 インターフェイス](isymunmanagedwriter3-interface.md)
- [OpenMethod メソッド](isymunmanagedwriter-openmethod-method.md)
