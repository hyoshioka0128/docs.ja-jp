---
title: ISymUnmanagedWriter インターフェイス
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter
helpviewer_keywords:
- ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: 7d6733ec-f081-4166-bc17-de09e16dc304
topic_type:
- apiref
ms.openlocfilehash: 8f0bbd26bde562df5482d167c9d2775e01426f55
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610055"
---
# <a name="isymunmanagedwriter-interface"></a>ISymUnmanagedWriter インターフェイス
シンボルライターを表し、ドキュメント、シーケンスポイント、構文スコープ、および変数を定義するメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Abort メソッド](isymunmanagedwriter-abort-method.md)|シンボルストアにシンボルをコミットせずにシンボルライターを閉じます。|  
|[Close メソッド](isymunmanagedwriter-close-method.md)|シンボルをシンボルストアにコミットした後、シンボルライターを閉じます。|  
|[CloseMethod メソッド](isymunmanagedwriter-closemethod-method.md)|現在のメソッドを閉じます。 メソッドを閉じると、それ以上シンボルを定義することはできません。|  
|[CloseNamespace メソッド](isymunmanagedwriter-closenamespace-method.md)|最近開いた名前空間を閉じます。|  
|[CloseScope メソッド](isymunmanagedwriter-closescope-method.md)|現在の構文のスコープを閉じます。|  
|[DefineConstant メソッド](isymunmanagedwriter-defineconstant-method.md)|定数値の名前を定義します。|  
|[DefineDocument メソッド](isymunmanagedwriter-definedocument-method.md)|ソース ドキュメントを定義します。|  
|[DefineField メソッド](isymunmanagedwriter-definefield-method.md)|メソッド内にない単一の変数を定義します。|  
|[DefineGlobalVariable メソッド](isymunmanagedwriter-defineglobalvariable-method.md)|グローバル変数を 1 つ定義します。|  
|[DefineLocalVariable メソッド](isymunmanagedwriter-definelocalvariable-method.md)|現在の構文のスコープの変数を 1 つ定義します。|  
|[DefineParameter メソッド](isymunmanagedwriter-defineparameter-method.md)|現在のメソッドのパラメーターを 1 つ定義します。|  
|[DefineSequencePoints メソッド](isymunmanagedwriter-definesequencepoints-method.md)|現在のメソッド内のシーケンス ポイントのグループを定義します。|  
|[GetDebugInfo メソッド](isymunmanagedwriter-getdebuginfo-method.md)|コンパイラがポータブル実行可能 (PE) ファイルヘッダーにデバッグディレクトリエントリを書き込むために必要な情報を返します。|  
|[Initialize メソッド](isymunmanagedwriter-initialize-method.md)|このライターが関連付けられるメタデータエミッタインターフェイスを設定し、デバッグシンボルの書き込み先となる出力ファイル名を設定します。|  
|[Initialize2 メソッド](isymunmanagedwriter-initialize2-method.md)|このライターが関連付けられるメタデータエミッタインターフェイスを設定し、デバッグシンボルの書き込み先となる出力ファイル名を設定し、プログラムデータベース (PDB) ファイルの最終的な場所を設定します。|  
|[OpenMethod メソッド](isymunmanagedwriter-openmethod-method.md)|シンボル情報を出力するメソッドを開きます。|  
|[OpenNamespace メソッド](isymunmanagedwriter-opennamespace-method.md)|新しい名前空間を開きます。|  
|[OpenScope メソッド](isymunmanagedwriter-openscope-method.md)|現在のメソッドの構文の新しいスコープを開きます。|  
|[RemapToken メソッド](isymunmanagedwriter-remaptoken-method.md)|メタデータが生成されたときにメタデータトークンが再マップされたことをシンボルライターに通知します。|  
|[SetMethodSourceRange メソッド](isymunmanagedwriter-setmethodsourcerange-method.md)|ソース ファイル内にメソッドの実際の先頭と末尾を指定します。|  
|[SetScopeRange メソッド](isymunmanagedwriter-setscoperange-method.md)|指定した構文のスコープのオフセット範囲を定義します。|  
|[SetSymAttribute メソッド](isymunmanagedwriter-setsymattribute-method.md)|名前に基づいてカスタム属性を定義します。|  
|[SetUserEntryPoint メソッド](isymunmanagedwriter-setuserentrypoint-method.md)|このモジュールのエントリポイントであるユーザー定義メソッドを指定します。|  
|[UsingNamespace メソッド](isymunmanagedwriter-usingnamespace-method.md)|現在開いている構文のスコープ内で、指定された完全修飾名前空間名が使用されていることを指定します。|  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** CorSym .idl、CorSym .h  
  
## <a name="see-also"></a>関連項目

- [シンボル ストア診断インターフェイス](diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedWriter2 インターフェイス](isymunmanagedwriter2-interface.md)
- [ISymUnmanagedWriter3 インターフェイス](isymunmanagedwriter3-interface.md)
