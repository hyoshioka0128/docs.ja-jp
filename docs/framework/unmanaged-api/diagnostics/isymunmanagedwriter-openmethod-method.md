---
title: ISymUnmanagedWriter::OpenMethod メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.OpenMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::OpenMethod
helpviewer_keywords:
- ISymUnmanagedWriter::OpenMethod method [.NET Framework debugging]
- OpenMethod method [.NET Framework debugging]
ms.assetid: fb90cb7f-af88-45e8-a99f-80a0bbddb08b
topic_type:
- apiref
ms.openlocfilehash: d2d16ab0a29fadd3a64d906a64fc46c422e01c45
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610042"
---
# <a name="isymunmanagedwriteropenmethod-method"></a>ISymUnmanagedWriter::OpenMethod メソッド
シンボル情報を出力するメソッドを開きます。 指定されたメソッドは、シーケンスポイント、パラメーター、および構文のスコープを定義するための呼び出しの現在のメソッドになります。 メソッド全体を囲む構文の暗黙的なスコープがあります。 以前に閉じられたメソッドを再度開くと、そのメソッドに対して定義されていたシンボルはすべて消去されます。 開いているメソッドは一度に1つしか存在できません。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT OpenMethod(  
    [in] mdMethodDef method);  
```  
  
## <a name="parameters"></a>パラメーター  
 `method`  
 から開くメソッドのメタデータトークン。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
- [CloseMethod メソッド](isymunmanagedwriter-closemethod-method.md)
- [OpenMethod2 メソッド](isymunmanagedwriter3-openmethod2-method.md)
