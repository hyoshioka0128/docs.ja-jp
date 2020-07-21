---
title: -win32res (C# コンパイラ オプション)
ms.date: 07/20/2015
f1_keywords:
- /win32res
helpviewer_keywords:
- win32res compiler option
- /win32res compiler option [C#]
- -win32res compiler option [C#]
- win32res compiler option [C#]
ms.assetid: 3c33f750-6948-4c7e-a27e-bef98f77255b
ms.openlocfilehash: 3bb1614fcf28c62a9000c9b96af2f046f329fb1e
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82794378"
---
# <a name="-win32res-c-compiler-options"></a>-win32res (C# コンパイラ オプション)
**-win32res** オプションは、Win32 リソースを出力ファイルに挿入します。  
  
## <a name="syntax"></a>構文  
  
```console  
-win32res:filename  
```  
  
## <a name="arguments"></a>引数  
 `filename`  
 出力ファイルに追加するリソース ファイル。  
  
## <a name="remarks"></a>Remarks  
 Win32 リソース ファイルは、[リソース コンパイラ](resource-compiler-option.md)を使用して作成できます。 リソース コンパイラは、Visual C++ プログラムをコンパイルするときに呼び出されます。 .res ファイルは .rc ファイルから作成されます。  
  
 Win32 リソースは、バージョンまたはビットマップ (アイコン) 情報を格納できます。エクスプローラーでアプリケーションを識別するのに役立ちます。 **-win32res** を指定しない場合、コンパイラはアセンブリ バージョンに基づいてバージョン情報を生成します。  
  
 .NET Framework リソース ファイルの [-linkresource](./linkresource-compiler-option.md) (参照) または [-resource](./resource-compiler-option.md) (アタッチ) をご覧ください。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 開発環境でこのコンパイラ オプションを設定するには  
  
1. プロジェクトの **[プロパティ]** ページを開きます。  
  
2. **[アプリケーション]** プロパティ ページをクリックします。  
  
3. **[リソース ファイル]** ボタンをクリックし、コンボ ボックスを利用してファイルを選択します。  
  
## <a name="example"></a>例  
 `in.cs` をコンパイルし、Win32 リソース ファイル `rf.res` をアタッチし、`in.exe` を作成します。  
  
```console  
csc -win32res:rf.res in.cs  
```  
  
## <a name="see-also"></a>関連項目

- [C# コンパイラ オプション](./index.md)
- [プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)
