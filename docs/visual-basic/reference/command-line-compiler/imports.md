---
title: -imports
ms.date: 03/10/2018
helpviewer_keywords:
- /imports compiler option [Visual Basic]
- imports compiler option [Visual Basic]
- -imports compiler option [Visual Basic]
ms.assetid: 9a93fb53-c080-497b-bf9b-441022dbbc39
ms.openlocfilehash: cc9fc222843bdfe8e49d2d291dc36ff3e0c63fc2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408596"
---
# <a name="-imports-visual-basic"></a>-imports (Visual Basic)
指定されたアセンブリから名前空間をインポートします。  
  
## <a name="syntax"></a>構文  
  
```console  
-imports:namespaceList  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`namespaceList`|必須です。 インポートされる名前空間のコンマ区切りの一覧。|  
  
## <a name="remarks"></a>Remarks  
 `-imports` オプションでは、参照アセンブリから、あるいはソース ファイルの現在のセット内に定義されている名前空間をインポートします。  
  
 `-imports` で指定された名前空間のメンバーは、コンパイル時にすべてのソースコード ファイルで使用できます。 単一のソースコード ファイルで名前空間を使用するには、[ ステートメント (.NET 名前空間および型)](../../language-reference/statements/imports-statement-net-namespace-and-type.md) を使用します。  
  
|Visual Studio 統合開発環境で -imports を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[参照]** タブをクリックします。<br />3. **[ユーザー インポートの追加]** ボタンの横にあるボックスに、名前空間の名前を入力します。<br />4. **[ユーザー インポートの追加]** ボタンをクリックします。|  
  
## <a name="example"></a>例  
 `-imports:system.globalization` が指定されている場合、次のコードがコンパイルされます。 それがない場合、正常にコンパイルするには、ソース コード ファイルの先頭に `Imports System.Globalization` ステートメントを含めるか、プロパティを `System.Globalization.CultureInfo.CurrentCulture.Name` として完全に修飾する必要があります。

```vb
Module Example
   Public Sub Main()
      Console.WriteLine($"The current culture is {CultureInfo.CurrentCulture.Name}")
   End Sub
End Module
```

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [参照と Imports ステートメント](../../programming-guide/program-structure/references-and-the-imports-statement.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
