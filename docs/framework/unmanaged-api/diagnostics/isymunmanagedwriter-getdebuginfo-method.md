---
title: ISymUnmanagedWriter::GetDebugInfo メソッド
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.GetDebugInfo
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::GetDebugInfo
helpviewer_keywords:
- ISymUnmanagedWriter::GetDebugInfo method [.NET Framework debugging]
- GetDebugInfo method [.NET Framework debugging]
ms.assetid: dd31c210-6829-45eb-927e-cc53932638b7
topic_type:
- apiref
ms.openlocfilehash: f8eb4cb6bad95295e10a72812fa8dbb0adfcc898
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614787"
---
# <a name="isymunmanagedwritergetdebuginfo-method"></a>ISymUnmanagedWriter::GetDebugInfo メソッド
コンパイラがポータブル実行可能 (PE) ファイルヘッダーにデバッグディレクトリエントリを書き込むために必要な情報を返します。 シンボルライターは、およびを除くすべてのフィールドを入力し `TimeDateStamp` `PointerToRawData` ます。 (コンパイラは、これらの2つのフィールドを適切に設定する必要があります)。  
  
 コンパイラは、このメソッドを呼び出し、PE ファイルにデータ blob を出力します。次に、 `PointerToRawData` 生成されたデータを指すように IMAGE_DEBUG_DIRECTORY のフィールドを設定し、IMAGE_DEBUG_DIRECTORY を pe ファイルに書き込みます。 また、コンパイラは、 `TimeDateStamp` `TimeDateStamp` 生成される PE ファイルのと同じフィールドをに設定する必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetDebugInfo(  
    [in, out] IMAGE_DEBUG_DIRECTORY *pIDD,  
    [in]  DWORD cData,  
    [out] DWORD *pcData,  
    [out, size_is(cData),  
        length_is(*pcData)] BYTE data[]);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pIDD`  
 [入力、出力]シンボルライターが入力する IMAGE_DEBUG_DIRECTORY へのポインター。  
  
 `cData`  
 から`DWORD`デバッグデータのサイズを格納している。  
  
 `pcData`  
 入出力`DWORD`デバッグデータを格納するために必要なバッファーのサイズを受け取るへのポインター。  
  
 `data`  
 入出力シンボルストアのデバッグデータを保持するのに十分な大きさのバッファーへのポインター。  
  
## <a name="return-value"></a>戻り値  
 メソッドが成功した場合は S_OK。それ以外の場合は、E_FAIL またはその他のエラーコードを指定します。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [ISymUnmanagedWriter インターフェイス](isymunmanagedwriter-interface.md)
