---
title: -win32icon
ms.date: 03/13/2018
helpviewer_keywords:
- win32icon compiler option [Visual Basic]
- -win32icon compiler option [Visual Basic]
- /win32icon compiler option [Visual Basic]
ms.assetid: aecaab01-9353-46c5-941c-6edabd4eff92
ms.openlocfilehash: 52ef0b991554c800dba4320b0c64c81ddd1b0ff4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414286"
---
# <a name="-win32icon"></a>-win32icon
.ico ファイルを出力ファイルに挿入します。 この .ico ファイルは、**エクスプローラー**では出力ファイルを表します。  
  
## <a name="syntax"></a>構文  
  
```console  
-win32icon:filename  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`filename`|出力ファイルに追加する .ico ファイル。 ファイル名に空白が含まれている場合は、名前を二重引用符 (" ") で囲みます。|  
  
## <a name="remarks"></a>Remarks  
 Microsoft Windows リソース コンパイラ (RC) を使用して .ico ファイルを作成することができます。 リソース コンパイラは、Visual C++ プログラムをコンパイルするときに呼び出されます。 .ico ファイルは .rc ファイルから作成されます。 `-win32icon` オプションと `-win32resource` オプションは同時に指定できません。  
  
 .NET Framework リソース ファイルの参照については「[-linkresource (Visual Basic)](linkresource.md)」を、.NET Framework リソース ファイルのアタッチについては「[-resource (Visual Basic)](resource.md)」を参照してください。 .res ファイルのインポートについては、「[-win32resource](win32resource.md)」を参照してください。  
  
|Visual Studio IDE で -win32icon を設定するには|  
|---|  
|1.**ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 <br />2. **[アプリケーション]** タブをクリックします。<br />3. **[アイコン]** ボックスの値を変更します。|  
  
## <a name="example"></a>例  
 次のコードでは `In.vb` がコンパイルされ、.ico ファイル `Rf.ico` がアタッチされます。  
  
```console
vbc -win32icon:rf.ico in.vb  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
