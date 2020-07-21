---
title: ISymUnmanagedReader::GetUserEntryPoint メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetUserEntryPoint
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetUserEntryPoint
helpviewer_keywords:
- GetUserEntryPoint method [.NET Framework debugging]
- ISymUnmanagedReader::GetUserEntryPoint method [.NET Framework debugging]
ms.assetid: 3fd3a34c-d176-46e9-9996-fb1646cff9b0
topic_type:
- apiref
ms.openlocfilehash: d465f830fa73016c3cf3f7df3a4a4d0c42bc0980
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615502"
---
# <a name="isymunmanagedreadergetuserentrypoint-method"></a>ISymUnmanagedReader::GetUserEntryPoint メソッド
モジュールのユーザーエントリポイントとして指定されたメソッド (存在する場合) を返します。 たとえば、このメソッドは、main メソッドの前にコンパイラで生成されたスタブではなく、ユーザーのメインメソッドである可能性があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetUserEntryPoint (  
    [out, retval]  mdMethodDef  *pToken);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pToken`  
 入出力エントリポイントを受け取る変数へのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedReader インターフェイス](isymunmanagedreader-interface.md)
