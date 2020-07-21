---
title: -verbose
ms.date: 03/13/2018
helpviewer_keywords:
- verbose compiler option [Visual Basic]
- -verbose compiler option [Visual Basic]
- /verbose compiler option [Visual Basic]
ms.assetid: d1aec0c1-0261-421d-9adc-5b13756100be
ms.openlocfilehash: 405b557568a736de3ddc3b51e265261222613131
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403032"
---
# <a name="-verbose"></a>-verbose
コンパイラによって詳細なステータス メッセージとエラー メッセージが生成されるようにします。  
  
## <a name="syntax"></a>構文  
  
```console  
-verbose[+ | -]  
```  
  
## <a name="arguments"></a>引数  
 `+` &#124; `-`  
 任意。 `-verbose` を指定することは、`-verbose+` を指定することと同じです。これにより、コンパイラで詳細なメッセージが出力されます。 このオプションの既定値は `-verbose-` です。  
  
## <a name="remarks"></a>Remarks  
 `-verbose` オプションでは、コンパイラによって発行されたエラーの合計数に関する情報を表示し、どのアセンブリがモジュールに読み込まれているかを報告します。また、どのファイルが現在コンパイルされているかを表示します。  
  
> [!NOTE]
> `-verbose` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。  
  
## <a name="example"></a>例  
 次のコードでは `In.vb` がコンパイルされ、詳細情報を表示するようにコンパイラに指示されます。  
  
```console  
vbc -verbose in.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
