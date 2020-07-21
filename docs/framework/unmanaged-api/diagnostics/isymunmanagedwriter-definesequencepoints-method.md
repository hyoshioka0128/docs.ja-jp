---
title: ISymUnmanagedWriter::DefineSequencePoints メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineSequencePoints
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineSequencePoints
helpviewer_keywords:
- DefineSequencePoints method [.NET Framework debugging]
- ISymUnmanagedWriter::DefineSequencePoints method [.NET Framework debugging]
ms.assetid: 64202baf-be6b-40ba-8162-8cc6c0c9b8e1
topic_type:
- apiref
ms.openlocfilehash: 8889c412f414f38d1d18d33ec297e82fd052280d
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614800"
---
# <a name="isymunmanagedwriterdefinesequencepoints-method"></a>ISymUnmanagedWriter::DefineSequencePoints メソッド
現在のメソッド内のシーケンス ポイントのグループを定義します。 開始行と開始列はそれぞれ、メソッド内のステートメントの開始を定義します。 各終了行と終了列は、メソッド内のステートメントの末尾を定義します。 配列は、オフセットの昇順で並べ替える必要があります。 オフセットは、常にメソッドの先頭からバイト単位で測定されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DefineSequencePoints(  
    [in] ISymUnmanagedDocumentWriter*  document,  
    [in] ULONG32 spCount,  
    [in, size_is(spCount)] ULONG32     offsets[],  
    [in, size_is(spCount)] ULONG32     lines[],  
    [in, size_is(spCount)] ULONG32     columns[],  
    [in, size_is(spCount)] ULONG32     endLines[],  
    [in, size_is(spCount)] ULONG32     endColumns[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `document`  
 からシーケンスポイントが定義されているドキュメントオブジェクト。  
  
 `spCount`  
 から、、 `ULONG32` `offsets` `lines` `columns` 、 `endLines` 、および `endColumns` の各バッファーのサイズを示す。  
  
 `offsets`  
 からメソッドの先頭から計測されたシーケンスポイントのオフセット。  
  
 `lines`  
 からシーケンスポイントの開始行番号。  
  
 `columns`  
 からシーケンスポイントの開始列番号。  
  
 `endLines`  
 からシーケンスポイントの終了行番号。 このパラメーターは省略可能です。  
  
 `endColumns`  
 からシーケンスポイントの終了列番号。 このパラメーターは省略可能です。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
