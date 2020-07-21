---
title: -nostdlib
ms.date: 03/13/2018
helpviewer_keywords:
- nostdlib compiler option [Visual Basic]
- -nostdlib compiler option [Visual Basic]
- /nostdlib compiler option [Visual Basic]
ms.assetid: 140381b8-dc96-4ad5-ae11-792c9ed0be4d
ms.openlocfilehash: 0934799853323110e73087ba6d8975c30f84d8f7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387713"
---
# <a name="-nostdlib-visual-basic"></a>-nostdlib (Visual Basic)
コンパイラが標準ライブラリを自動的に参照しないようにします。  
  
## <a name="syntax"></a>構文  
  
```console  
-nostdlib  
```  
  
## <a name="remarks"></a>Remarks  
 `-nostdlib` オプションを指定すると、System.dll アセンブリへの自動参照が削除され、コンパイラで Vbc.rsp ファイルを読み取れないようにします。 Vbc.rsp ファイルは、Vbc.exe ファイルと同じディレクトリにあり、一般的に使用される .NET Framework アセンブリを参照し、`System` と `Microsoft.VisualBasic` の名前空間をインポートします。  
  
> [!NOTE]
> Mscorlib.dll アセンブリおよび Microsoft.VisualBasic.dll アセンブリは常に参照されます。  
  
> [!NOTE]
> `-nostdlib` オプションは、Visual Studio 開発環境からは利用できません。これはコマンド ラインからコンパイルするときにのみ使用できます。  
  
## <a name="example"></a>例  
 次のコードでは、標準ライブラリを参照されずに `T2.vb` がコンパイルされます。 `My` オブジェクトを削除するには、`_MYTYPE` 条件付きコンパイル定数を文字列 "Empty" に設定する必要があります。  
  
```console
vbc -nostdlib -define:_MYTYPE=\"Empty\" T2.vb  
```  
  
## <a name="see-also"></a>関連項目

- [-noconfig](noconfig.md)
- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [My で利用可能なオブジェクトのカスタマイズ](../../developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)
