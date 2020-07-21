---
title: ISymUnmanagedDocument インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument
helpviewer_keywords:
- ISymUnmanagedDocument interface [.NET Framework debugging]
ms.assetid: 5c26b366-6e81-467c-9dd0-02dd26fee0a3
topic_type:
- apiref
ms.openlocfilehash: a8ff6d3a925773e58e0713a87b167420c246f85b
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615567"
---
# <a name="isymunmanageddocument-interface"></a>ISymUnmanagedDocument インターフェイス
シンボル ストアによって参照されるドキュメントを表します。 ドキュメントは、URL (uniform resource locator) とドキュメントの種類の GUID によって定義されます。 URL とドキュメントの種類の GUID を使用して、ドキュメントがどのように格納されているかに関係なく、ドキュメントを見つけることができます。 ドキュメントソースをシンボルストアに格納し、このインターフェイスを使用して取得することができます。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[FindClosestLine メソッド](isymunmanageddocument-findclosestline-method.md)|このドキュメント内の行が指定されている場合は、シーケンスポイントで最も近い行を返します。|  
|[GetCheckSum メソッド](isymunmanageddocument-getchecksum-method.md)|チェックサムを取得します。|  
|[GetCheckSumAlgorithmId メソッド](isymunmanageddocument-getchecksumalgorithmid-method.md)|チェックサムアルゴリズム識別子を取得します。チェックサムがない場合は、すべての0の GUID を返します。|  
|[GetDocumentType メソッド](isymunmanageddocument-getdocumenttype-method.md)|このドキュメントのドキュメントの種類を取得します。|  
|[GetLanguage メソッド](isymunmanageddocument-getlanguage-method.md)|このドキュメントの言語識別子を取得します。|  
|[GetLanguageVendor メソッド](isymunmanageddocument-getlanguagevendor-method.md)|このドキュメントの言語販売元を取得します。|  
|[GetSourceLength メソッド](isymunmanageddocument-getsourcelength-method.md)|埋め込まれたソースの長さをバイト数で取得します。|  
|[GetSourceRange メソッド](isymunmanageddocument-getsourcerange-method.md)|指定されたバッファーに、埋め込みソースの指定された範囲を返します。|  
|[GetURL メソッド](isymunmanageddocument-geturl-method.md)|このドキュメントの URL を返します。|  
|[HasEmbeddedSource メソッド](isymunmanageddocument-hasembeddedsource-method.md)|`true`ドキュメントがデバッグシンボルに埋め込まれている場合はを返します。それ以外の場合はを返し `false` ます。|  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
