---
title: -langversion
ms.date: 03/10/2018
helpviewer_keywords:
- /langversion compiler option [Visual Basic]
- langversion compiler option [Visual Basic]
- -langversion compiler option [Visual Basic]
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
ms.openlocfilehash: 271606ac021e6afcb28fdac3e1bc86e1aaba7d2b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408539"
---
# <a name="-langversion-visual-basic"></a>-langversion (Visual Basic)
コンパイラで、指定した Visual Basic 言語バージョンに含まれている構文のみが受け入れられるようにします。  
  
## <a name="syntax"></a>構文  
  
```console  
-langversion:version  
```  
  
## <a name="arguments"></a>引数  
 `version`  
 必須です。 コンパイル中に使用される言語バージョン。 指定できる値は、`9`、`10`、`11`、`12`、`14`、`15`、`15.3`、`15.5`、`default`、`latest` です。

 `.0` をマイナー バージョンとして使用して、整数値を指定することもできます (`11.0` など)。

 使用可能なすべての値の一覧を表示するには、コマンド ラインで `-langversion:?` を指定します。  
  
## <a name="remarks"></a>Remarks  
 `-langversion` オプションは、コンパイラで受け入れられる構文を指定します。 たとえば、言語バージョンが 9.0 であることを指定した場合、コンパイラではバージョン 10.0 以降でのみ有効な構文に対してエラーが生成されます。  
  
 このオプションは、異なるバージョンの .NET Framework をターゲットとするアプリケーションを開発する場合に使用できます。 たとえば、.NET Framework 3.5 をターゲットとしている場合は、このオプションを使用して、言語バージョン 10.0 の構文を確実に使用しないようにすることができます。  
  
 `-langversion` を直接設定するには、コマンド ラインを使用する必要があります。 詳細については、「[対象となる特定の .NET Framework のバージョンの指定](/visualstudio/ide/visual-studio-multi-targeting-overview)」を参照してください。  
  
## <a name="example"></a>例  
 次のコードでは、Visual Basic 9.0 の `sample.vb` がコンパイルされます。  
  
```console  
vbc -langversion:9.0 sample.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [対象となる特定の .NET Framework バージョンの指定](/visualstudio/ide/visual-studio-multi-targeting-overview)
