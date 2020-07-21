---
title: -utf8output
ms.date: 07/20/2015
helpviewer_keywords:
- -utf8output compiler option [Visual Basic]
- utf8output compiler option [Visual Basic]
- /utf8output compiler option [Visual Basic]
ms.assetid: 8ab36b1e-027a-49ac-85b4-f48997d9e4d6
ms.openlocfilehash: 0a16cdc535de5ed0619bf080bb4637449b11cfef
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403058"
---
# <a name="-utf8output-visual-basic"></a>-utf8output (Visual Basic)
UTF-8 エンコードを使用してコンパイラ出力を表示します。  
  
## <a name="syntax"></a>構文  
  
```console  
-utf8output[+ | -]  
```  
  
## <a name="arguments"></a>引数  
 `+` &#124; `-`  
 任意。 このオプションの既定値は `-utf8output-` です。これは、コンパイラ出力で UTF-8 エンコードが使用されないことを意味します。 `-utf8output` を指定することは、`-utf8output+` を指定することと同じです。  
  
## <a name="remarks"></a>Remarks  
 地域と言語の構成によっては、コンパイラ出力をコンソールに正しく表示できない場合があります。 このような場合は、`-utf8output` を使用して、コンパイラ出力をファイルにリダイレクトします。  
  
> [!NOTE]
> `-utf8output` オプションは、Visual Studio 開発環境内からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。  
  
## <a name="example"></a>例  
 次のコードでは `In.vb` をコンパイルし、UTF-8 エンコードを使用して出力を表示するようにコンパイラに指示します。  
  
```console  
vbc -utf8output in.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
