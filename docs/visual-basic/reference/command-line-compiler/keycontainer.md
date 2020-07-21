---
title: -keycontainer
ms.date: 03/10/2018
helpviewer_keywords:
- -keycontainer compiler option [Visual Basic]
- keycontainer compiler option [Visual Basic]
- /keycontainer compiler option [Visual Basic]
ms.assetid: 6a9bc861-1752-4db1-9f64-b5252f0482cc
ms.openlocfilehash: 575b337c262fbb36a9e118aa293916c296cc2db3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408563"
---
# <a name="-keycontainer"></a>-keycontainer
アセンブリに厳密な名前を付けるキー ペアのキー コンテナー名を指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-keycontainer:container  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`container`|必須です。 キーが格納されているコンテナー ファイル。 ファイル名に空白が含まれている場合は、名前を二重引用符 ("") で囲みます。|  
  
## <a name="remarks"></a>Remarks  
 コンパイラにより、アセンブリ マニフェストに公開キーが挿入され、秘密キーで最終アセンブリに署名されて、共有可能なコンポーネントが作成されます。 キー ファイルを生成するには、コマンド ラインで「`sn -k file`」と入力します。 `-i` オプションでは、キー ペアがコンテナーにインストールされます。 詳細については、「[Sn.exe (厳密名ツール)](../../../framework/tools/sn-exe-strong-name-tool.md)」を参照してください。  
  
 `-target:module` を指定してコンパイルした場合は、キー ファイルの名前はモジュールに保持され、[-addmodule](addmodule.md) を使用してコンパイルして作成したアセンブリに組み込まれます。  
  
 このオプションは、任意の Microsoft Intermediate Language (MSIL) モジュールのソース コードで、カスタム属性 (<xref:System.Reflection.AssemblyKeyNameAttribute>) として指定することもできます。  
  
 また、暗号化情報を [-keyfile](keyfile.md) でコンパイラに渡すことができます。 部分的に署名されたアセンブリを作成する場合は、[-delaysign](delaysign.md) を使います。  
  
 アセンブリへの署名の詳細については、「[厳密な名前付きアセンブリの作成と使用](../../../standard/assembly/create-use-strong-named.md)」を参照してください。  
  
> [!NOTE]
> `-keycontainer` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。  
  
## <a name="example"></a>例  
 次のコードでは、ソース ファイル `Input.vb` がコンパイルされ、キー コンテナーが指定されます。  
  
```console  
vbc -keycontainer:key1 input.vb  
```  
  
## <a name="see-also"></a>関連項目

- [.NET のアセンブリ](../../../standard/assembly/index.md)
- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-keyfile](keyfile.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
