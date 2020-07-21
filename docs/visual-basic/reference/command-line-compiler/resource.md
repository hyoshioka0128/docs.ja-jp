---
title: -resource
ms.date: 03/13/2018
helpviewer_keywords:
- /resource compiler option [Visual Basic]
- -resource compiler option [Visual Basic]
- /res compiler option [Visual Basic]
- res compiler option [Visual Basic]
- -res compiler option [Visual Basic]
- resource compiler option [Visual Basic]
ms.assetid: eee2f227-91f2-4f2b-a9d6-1c51c5320858
ms.openlocfilehash: cf9fe8dae0d35df694891633a6e3cf950bfb7376
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363618"
---
# <a name="-resource-visual-basic"></a>-resource (Visual Basic)
マネージド リソースをアセンブリに埋め込みます。  
  
## <a name="syntax"></a>構文  
  
```console  
-resource:filename[,identifier[,public|private]]  
```

or  

```console
-res:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`filename`|必須です。 出力ファイルに埋め込まれるリソース ファイルの名前。 既定では、アセンブリで `filename` はパブリックとなります。 ファイル名に空白が含まれている場合は、名前を二重引用符 (" ") で囲みます。|  
|`identifier`|任意。 リソースの論理名。その読み込みに使用される名前。 既定値は、ファイルの名前です。 必要に応じて、次のように、アセンブリ マニフェストでリソースをパブリックとプライベートのどちらにするかを指定できます: `-res:filename.res, myname.res, public`|  
  
## <a name="remarks"></a>Remarks  
 リソース ファイルを出力ファイルに配置せずに、リソースをアセンブリにリンクするには、`-linkresource` を使用します。  
  
 `filename` が [Resgen.exe (リソース ファイル ジェネレーター)](../../../framework/tools/resgen-exe-resource-file-generator.md) や開発環境などで作成された .NET Framework リソース ファイルである場合は、<xref:System.Resources> 名前空間のメンバーを使用してアクセスできます (詳細については、<xref:System.Resources.ResourceManager> を参照)。 実行時に他のすべてのリソースにアクセスするには、<xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>、<xref:System.Reflection.Assembly.GetManifestResourceNames%2A>、または <xref:System.Reflection.Assembly.GetManifestResourceStream%2A> のいずれかのメソッドを使用します。  
  
 `-resource` の省略形は `-res` です。  
  
 Visual Studio IDE で `-resource` を設定する方法については、「[アプリケーション リソースの管理 (.NET)](/visualstudio/ide/managing-application-resources-dotnet)」を参照してください。  
  
## <a name="example"></a>例  
 次のコードでは `In.vb` をコンパイルし、リソース ファイル `Rf.resource` をアタッチします。  
  
```console
vbc -res:rf.resource in.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-win32resource](win32resource.md)
- [-linkresource (Visual Basic)](linkresource.md)
- [-target (Visual Basic)](target.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
