---
title: -doc
ms.date: 03/10/2018
helpviewer_keywords:
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
ms.openlocfilehash: 57a81983278c26090c62995f4da55c5cbfd66047
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408674"
---
# <a name="-doc"></a>-doc
ドキュメント コメントを XML ファイルに出力します。  
  
## <a name="syntax"></a>構文  
  
```console  
-doc[+ | -]  
```

or  

```console
-doc:file  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`+` &#124; `-`|任意。 +、または単に `-doc` を指定すると、コンパイラによってドキュメント情報が生成され、XML ファイル内に置かれます。 `-` を指定することは `-doc` を指定しないことと同じで、この場合ドキュメント情報は作成されません。|  
|`file`|`-doc:` を使用する場合に、必ず指定します。 出力の XML ファイルを指定します。これにはコンパイルのソース コード ファイルからのコメントが入力されます。 ファイル名に空白が含まれている場合は、名前を引用符 (" ") で囲みます。|  
  
## <a name="remarks"></a>Remarks  
 `-doc` オプションでは、コンパイラにドキュメント コメントを含む XML ファイルを生成させるかどうかを制御できます。 `-doc:file` 構文を使用する場合、`file` パラメーターによって XML ファイルの名前を指定します。 `-doc` または `-doc+` を使用する場合、コンパイラは、コンパイラが作成中の実行可能ファイルまたはライブラリから XML ファイルの名前を取得します。 `-doc-` を使用する場合、または `-doc` オプションを指定しない場合、コンパイラは XML ファイルを作成しません。  
  
 ソース コード ファイルで、ドキュメント コメントを次の定義の前に置くことができます。  
  
- [クラス](../../language-reference/statements/class-statement.md)や[インターフェイス](../../language-reference/statements/interface-statement.md)などのユーザー定義型  
  
- フィールド、[イベント](../../language-reference/statements/event-statement.md)、[プロパティ](../../language-reference/statements/property-statement.md)、[関数](../../language-reference/statements/function-statement.md)、[サブルーチン](../../language-reference/statements/sub-statement.md)などのメンバー。  
  
 Visual Studio [IntelliSense](/visualstudio/ide/using-intellisense) 機能で生成された XML ファイルを使用するには、XML ファイルの名前をサポートするアセンブリの名前と同じにします。 Visual Studio プロジェクトでアセンブリが参照されたときに .xml ファイルがうまく見つかるようにするために、XML ファイルがアセンブリと同じディレクトリにあることを確認します。 IntelliSense をプロジェクト内のコード、またはプロジェクトに参照されるプロジェクト内のコードに対して動作させるために、XML ドキュメント ファイルは必須ではありません。  
  
 `-target:module` を使用してコンパイルしない限り、XML ファイルにはタグ `<assembly></assembly>` が含まれます。 これらのタグでは、コンパイルの出力ファイルに向けたアセンブリ マニフェストを含むファイルの名前が指定されます。  
  
 コード内のコメントからドキュメントを生成する方法については、「[XML のコメント用タグ](../../language-reference/xmldoc/index.md)」をご覧ください。  
  
|Visual Studio 統合開発環境で -doc を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[コンパイル]** タブをクリックします。<br />3. **[XML ドキュメント ファイルを生成する]** ボックスに値を設定します。|  
  
## <a name="example"></a>例  
 サンプルについては、「[XML の使用によるコードのドキュメントの作成](../../programming-guide/program-structure/documenting-your-code-with-xml.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [XML の使用によるコードのドキュメントの作成](../../programming-guide/program-structure/documenting-your-code-with-xml.md)
