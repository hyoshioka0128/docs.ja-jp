---
title: -sdkpath
ms.date: 07/20/2015
f1_keywords:
- sdkpath
- -sdkpath
helpviewer_keywords:
- -sdkpath compiler option [Visual Basic]
- /sdkpath compiler option [Visual Basic]
- sdkpath compiler option [Visual Basic]
ms.assetid: fec8a3f1-b791-4a37-8af7-344859f8212d
ms.openlocfilehash: 85aba17b330af1b25b39f462844bc1a4856a448a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403110"
---
# <a name="-sdkpath"></a>-sdkpath
mscorlib.dll および Microsoft.VisualBasic.dll の場所を指定します。  
  
## <a name="syntax"></a>構文  
  
```console  
-sdkpath:path  
```  
  
## <a name="arguments"></a>引数  
 `path`  
 コンパイルに使用する mscorlib.dll と Microsoft.VisualBasic.dll のバージョンを格納しているディレクトリ。 このパスは、読み込まれるまで検証されません。 ディレクトリ名に空白が含まれている場合は、名前を二重引用符 (" ") で囲みます。  
  
## <a name="remarks"></a>Remarks  
 このオプションにより、Visual Basic コンパイラに対して、既定以外の場所から mscorlib.dll ファイルと Microsoft.VisualBasic.dll ファイルを読み込むように指示します。 `-sdkpath` オプションは、[-netcf](netcf.md) と共に使用するように設計されています。 .NET Compact Framework では、これらのサポート ライブラリのさまざまなバージョンを使用して、デバイスに見つからない型と言語機能の使用を回避します。  
  
> [!NOTE]
> `-sdkpath` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。 `-sdkpath` オプションは、Visual Basic デバイス プロジェクトが読み込まれるときに設定されます。  
  
 `-vbruntime` コンパイラ オプションを使うと、コンパイラで Visual Basic ランタイム ライブラリを参照せずにコンパイルすることを指定できます。 詳細については、「[-vbruntime](vbruntime.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコードでは、C ドライブ上の .NET Compact Framework の既定のインストール ディレクトリにある Mscorlib.dll と Microsoft.VisualBasic.dll のバージョンを使用して、.NET Compact Framework で `Myfile.vb` がコンパイルされます。 通常は、最新バージョンの .NET Compact Framework を使用します。  
  
```console
vbc -netcf -sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [-netcf](netcf.md)
- [-vbruntime](vbruntime.md)
