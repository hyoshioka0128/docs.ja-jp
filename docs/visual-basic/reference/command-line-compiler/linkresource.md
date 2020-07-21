---
title: -linkresource
ms.date: 03/10/2018
helpviewer_keywords:
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
ms.openlocfilehash: 43ebb61efa26ed11af573e2c4e73a6fd71ac0902
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403201"
---
# <a name="-linkresource-visual-basic"></a>-linkresource (Visual Basic)
マネージド リソースへのリンクを作成します。  
  
## <a name="syntax"></a>構文  
  
```console  
-linkresource:filename[,identifier[,public|private]]  
```

or  

```console
-linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>引数  
 `filename`  
 必須です。 アセンブリにリンクするリソース ファイル。 ファイル名に空白が含まれている場合は、名前を二重引用符で囲みます (" ")。  
  
 `identifier`  
 任意。 リソースの論理名。 リソースの読み込みに使用される名前。 既定値は、ファイルの名前です。 必要に応じて、アセンブリ マニフェストでファイルをパブリックとプライベートのどちらにするかを指定できます (例: `-linkres:filename.res,myname.res,public`)。 既定では、アセンブリで `filename` はパブリックとなります。  
  
## <a name="remarks"></a>Remarks  
 `-linkresource` オプションでは、リソース ファイルは出力ファイルに埋め込まれません。これを行うには、`-resource` オプションを使用します。  
  
 `-linkresource` オプションでは、`-target:module` 以外の `-target` オプションのいずれかが必要です。  
  
 `filename` が、たとえば [Resgen.exe (リソース ファイル ジェネレーター)](../../../framework/tools/resgen-exe-resource-file-generator.md) や開発環境で作成された .NET Framework リソース ファイルである場合は、<xref:System.Resources> 名前空間のメンバーを使用してアクセスできます (詳細は、<xref:System.Resources.ResourceManager> を参照)。実行時に他のすべてのリソースにアクセスするには、<xref:System.Reflection.Assembly> クラスの `GetManifestResource` で始まるメソッドを使用します。  
  
 ファイル名には任意のファイル形式を使用できます。 たとえば、ネイティブ DLL をアセンブリの一部にすることで、グローバル アセンブリ キャッシュにインストールして、アセンブリ内のマネージド コードからアクセスできるようにすることができます。  
  
 `-linkresource` の省略形は `-linkres` です。  
  
> [!NOTE]
> `-linkresource` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。  
  
## <a name="example"></a>例  
 次のコードでは `in.vb` がコンパイルされ、リソース ファイル `rf.resource` にリンクされます。  
  
```console  
vbc -linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-target (Visual Basic)](target.md)
- [-resource (Visual Basic)](resource.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
