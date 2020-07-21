---
title: ISymUnmanagedReader インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader
helpviewer_keywords:
- ISymUnmanagedReader interface [.NET Framework debugging]
ms.assetid: aa3cc15d-058e-4e6f-b03e-39569646ba47
topic_type:
- apiref
ms.openlocfilehash: b372021fcda39d9973d96a9c39e93e38617887a6
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615463"
---
# <a name="isymunmanagedreader-interface"></a>ISymUnmanagedReader インターフェイス
シンボルストア内のドキュメント、メソッド、および変数へのアクセスを提供するシンボルリーダーを表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetDocument メソッド](isymunmanagedreader-getdocument-method.md)|ドキュメントを検索します。|  
|[GetDocuments メソッド](isymunmanagedreader-getdocuments-method.md)|シンボルストアに定義されているすべてのドキュメントの配列を返します。|  
|[GetDocumentVersion メソッド](isymunmanagedreader-getdocumentversion-method.md)|指定したドキュメントの指定したバージョンを取得します。|  
|[GetGlobalVariables メソッド](isymunmanagedreader-getglobalvariables-method.md)|すべてのグローバル変数を返します。|  
|[GetMethod メソッド](isymunmanagedreader-getmethod-method.md)|メソッドトークンを指定して、シンボルリーダーメソッドを取得します。|  
|[GetMethodByVersion メソッド](isymunmanagedreader-getmethodbyversion-method.md)|メソッドトークンと編集およびコピーバージョン番号を指定して、シンボルリーダーメソッドを取得します。|  
|[GetMethodFromDocumentPosition メソッド](isymunmanagedreader-getmethodfromdocumentposition-method.md)|ドキュメント内の指定された位置にあるブレークポイントを含むメソッドを返します。|  
|[GetMethodsFromDocumentPosition メソッド](isymunmanagedreader-getmethodsfromdocumentposition-method.md)|メソッドの配列を返します。各メソッドには、ドキュメント内の指定された位置にあるブレークポイントが含まれています。|  
|[GetMethodVersion メソッド](isymunmanagedreader-getmethodversion-method.md)|メソッドのバージョンを取得します。|  
|[GetNamespaces メソッド](isymunmanagedreader-getnamespaces-method.md)|このシンボルストア内のグローバルスコープで定義されている名前空間を取得します。|  
|[GetSymAttribute メソッド](isymunmanagedreader-getsymattribute-method.md)|名前に基づいてカスタム属性を取得します。|  
|[GetSymbolStoreFileName メソッド](isymunmanagedreader-getsymbolstorefilename-method.md)|シンボルストアのディスク上のファイル名を提供します。|  
|[GetUserEntryPoint メソッド](isymunmanagedreader-getuserentrypoint-method.md)|モジュールのユーザーエントリポイントとして指定されたメソッド (存在する場合) を返します。|  
|[GetVariables メソッド](isymunmanagedreader-getvariables-method.md)|親と名前を指定して、非ローカル変数を返します。|  
|[Initialize メソッド](isymunmanagedreader-initialize-method.md)|このリーダーが関連付けられるメタデータインポーターインターフェイスと、モジュールのファイル名を使用して、シンボルリーダーを初期化します。|  
|[ReplaceSymbolStore メソッド](isymunmanagedreader-replacesymbolstore-method.md)|既存のシンボル ストアをデルタ シンボル ストアで置き換えます。|  
|[UpdateSymbolStore メソッド](isymunmanagedreader-updatesymbolstore-method.md)|既存のシンボル ストアをデルタ シンボル ストアで更新します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedReader2 インターフェイス](isymunmanagedreader2-interface.md)
