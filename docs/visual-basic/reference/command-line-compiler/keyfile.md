---
title: -keyfile
ms.date: 03/10/2018
helpviewer_keywords:
- /keyfile compiler option [Visual Basic]
- keyfile compiler option [Visual Basic]
- -keyfile compiler option [Visual Basic]
ms.assetid: ffa82a4b-517a-4c6c-9889-5bae7b534bb8
ms.openlocfilehash: 3f476f6b6db1a788002a938eb5ae4bbbed7a5dae
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408576"
---
# <a name="-keyfile"></a>-keyfile
アセンブリに厳密な名前を付けるキーまたはキー ペアを含むファイルを指定します。  
  
## <a name="syntax"></a>構文  
  
```console
-keyfile:file  
```  
  
## <a name="arguments"></a>引数  
 `file`  
 必須です。 キーが含まれるファイル。 ファイル名に空白が含まれている場合は、名前を二重引用符 (" ") で囲みます。  
  
## <a name="remarks"></a>Remarks  
 コンパイラでは、アセンブリ マニフェストに公開キーを挿入してから、秘密キーで最終的なアセンブリに署名します。 キー ファイルを生成するには、コマンド ラインで「`sn -k file`」と入力します。 詳細については、「[Sn.exe (厳密名ツール)](../../../framework/tools/sn-exe-strong-name-tool.md)」を参照してください。  
  
 `-target:module` を指定してコンパイルした場合は、キー ファイルの名前がモジュールに保持され、[-addmodule](addmodule.md) でアセンブリをコンパイルすると作成されるアセンブリに組み込まれます。  
  
 また、暗号化情報を [-keycontainer](keycontainer.md) でコンパイラに渡すことができます。 部分的に署名されたアセンブリを作成する場合は、[-delaysign](delaysign.md) を使います。  
  
 このオプションは、任意の Microsoft Intermediate Language モジュールのソース コードで、カスタム属性 (<xref:System.Reflection.AssemblyKeyFileAttribute>) として指定することもできます。  
  
 同じコンパイルで (コマンドライン オプションまたはカスタム属性によって) `-keyfile` と [-keycontainer](keycontainer.md) の両方が指定されている場合、コンパイラでは最初にキー コンテナーが試されます。 それが成功すると、アセンブリはキー コンテナーの情報で署名されます。 コンパイラでは、キー コンテナーが見つからない場合、`-keyfile` で指定されたファイルが試されます。 これが成功すると、アセンブリはキー ファイルの情報で署名され、キー情報はキー コンテナーにインストールされるため (`sn -i` と同様)、次のコンパイル時にはキー コンテナーが有効になります。  
  
 キー ファイルには公開キーだけが含まれる場合があることに注意してください。  
  
 アセンブリの署名の詳細については、「[厳密な名前付きアセンブリの作成と使用](../../../standard/assembly/create-use-strong-named.md)」を参照してください。  
  
> [!NOTE]
> `-keyfile` オプションは、Visual Studio 開発環境内からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。

## <a name="example"></a>例

次のコードでは、ソース ファイル `Input.vb` をコンパイルし、キー ファイルを指定します。

```console
vbc -keyfile:myfile.sn input.vb
```

## <a name="see-also"></a>関連項目

- [.NET のアセンブリ](../../../standard/assembly/index.md)
- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-reference (Visual Basic)](reference.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
