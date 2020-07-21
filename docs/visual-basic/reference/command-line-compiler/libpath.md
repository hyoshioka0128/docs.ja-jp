---
title: -libpath
ms.date: 03/10/2018
helpviewer_keywords:
- libpath compiler option [Visual Basic]
- /libpath compiler option [Visual Basic]
- -libpath compiler option [Visual Basic]
ms.assetid: 5f1c26c9-3455-4e89-bdf3-b12d6c2e655b
ms.openlocfilehash: dff7e0c3eb696b9b18f4c4e59240a26c1cb9782c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408550"
---
# <a name="-libpath"></a>-libpath
参照アセンブリの場所を指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-libpath:dirList  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`dirList`|必須です。 参照されているアセンブリが現在の作業ディレクトリ (コンパイラの呼び出し元のディレクトリ) または共通言語ランタイムのシステム ディレクトリに見つからない場合に、コンパイラによって検索されるディレクトリのセミコロン区切りの一覧。 ディレクトリ名に空白が含まれている場合は、名前を二重引用符 (" ") で囲みます。|  
  
## <a name="remarks"></a>Remarks  
 `-libpath` オプションでは、[-reference](reference.md) オプションによって参照されるアセンブリの場所を指定します。  
  
 コンパイラは、完全に修飾されていないアセンブリ参照を次の順序で検索します。  
  
1. 現在の作業ディレクトリ。 これは、コンパイラを起動したディレクトリです。  
  
2. 共通言語ランタイムのシステム ディレクトリ。  
  
3. `-libpath` によって指定されているディレクトリ。  
  
4. LIB 環境変数によって指定されているディレクトリ。  
  
 `-libpath` オプションは付加的なものであり、複数回指定すると、前の値に追加されます。  
  
 アセンブリ参照を指定するには、`-reference` を使用します。  
  
|Visual Studio 統合開発環境で -libpath を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[参照]** タブをクリックします。<br />3. **[参照パス...]** ボタンをクリックします。<br />4. **[参照パス]** ダイアログ ボックスで、 **[フォルダー]** ボックスにディレクトリ名を入力します。<br />5. **[フォルダーの追加]** をクリックします。|  
  
## <a name="example"></a>例  
 次のコードでは、`T2.vb` をコンパイルして .exe ファイルを作成します。 コンパイラでは、作業ディレクトリ、C: ドライブのルート ディレクトリ、およびアセンブリ参照の C: ドライブの New Assemblies ディレクトリ内を検索します。  
  
```console  
vbc -libpath:c:\;"c:\New Assemblies" -reference:t2.dll t2.vb  
```  
  
## <a name="see-also"></a>関連項目

- [.NET のアセンブリ](../../../standard/assembly/index.md)
- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
