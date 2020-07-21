---
title: -warnaserror
ms.date: 03/13/2018
helpviewer_keywords:
- warnaserror compiler option [Visual Basic]
- /warnaserror compiler option [Visual Basic]
- -warnaserror compiler option [Visual Basic]
ms.assetid: 49819f1d-a1bd-4201-affe-5afe6d9712e1
ms.openlocfilehash: 94a8b43a891df9837925869e17fac4536a995264
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414273"
---
# <a name="-warnaserror-visual-basic"></a>-warnaserror (Visual Basic)
コンパイラで、最初に発生した警告がエラーとして扱われます。  
  
## <a name="syntax"></a>構文  
  
```console  
-warnaserror[+ | -][:numberList]  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|+ &#124; -|任意。 既定では `-warnaserror-` は有効です。警告が発生しても、コンパイラは出力ファイルを生成します。 `-warnaserror` オプションは `-warnaserror+` と同じで、警告がエラーとして扱われます。|  
|`numberList`|任意。 `-warnaserror` オプションを適用する、警告 ID 番号のコンマ区切りのリスト。 警告 ID が指定されていない場合、`-warnaserror`オプションはすべての警告に適用されます。|  
  
## <a name="remarks"></a>Remarks  
 `-warnaserror` オプションで、すべての警告がエラーとして扱われます。 通常は警告として報告されるすべてのメッセージが、代わりにエラーとして報告されます。 コンパイラは、後続の同じ警告の発生を警告として報告します。  
  
 既定では `-warnaserror-` が有効であり、警告は情報提供のみになります。 `-warnaserror` オプションは `-warnaserror+` と同じで、警告がエラーとして扱われます。  
  
 いくつかの特定の警告のみをエラーとして扱う場合は、エラーとして扱う警告番号のコンマ区切りのリストを指定できます。  
  
> [!NOTE]
> `-warnaserror` オプションでは、警告の表示方法は制御されません。 [-nowarn](nowarn.md) オプションを使用して警告を無効にします。  
  
|-warnaserror を設定し、Visual Studio IDE ですべての警告をエラーとして扱う|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[コンパイル]** タブをクリックします。<br />3. **[すべての警告を表示しない]** チェック ボックスがオフになっていることを確認します。<br />4. **[すべての警告をエラーとして扱う]** チェック ボックスをオンにします。|  
  
|-warnaserror を設定し、Visual Studio IDE で特定の警告をエラーとして扱う|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。<br />2. **[コンパイル]** タブをクリックします。<br />3. **[すべての警告を表示しない]** チェック ボックスがオフになっていることを確認します。<br />4. **[すべての警告をエラーとして扱う]** チェック ボックスがオフになっていることを確認します。<br />5.エラーとして扱う警告の隣にある **[通知]** 列から、 **[エラー]** を選択します。|  
  
## <a name="example"></a>例  
 次のコードは `In.vb` をコンパイルし、最初に見つけたすべての警告をエラーとして表示するようにコンパイラに指示します。  
  
```console
vbc -warnaserror in.vb  
```  
  
## <a name="example"></a>例  
 次のコードは `T2.vb` をコンパイルし、使用されていないローカル変数 (42024) に向けた警告のみをエラーとして扱います。  
  
```console
vbc -warnaserror:42024 t2.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)
