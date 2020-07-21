---
title: -main (C# コンパイラ オプション)
ms.date: 07/20/2015
f1_keywords:
- /main
helpviewer_keywords:
- -main compiler option [C#]
- main compiler option [C#]
- /main compiler option [C#]
ms.assetid: 975cf4d5-36ac-4530-826c-4aad0c7f2049
ms.openlocfilehash: 1de3d51953b632e3881db76202b63d3f287b39fe
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051871"
---
# <a name="-main-c-compiler-options"></a>-main (C# コンパイラ オプション)

このオプションは、**Main** メソッドを含むクラスが複数ある場合に、プログラムへのエントリ ポイントを含むクラスを指定します。

## <a name="syntax"></a>構文

```console
-main:class
```

## <a name="arguments"></a>引数
 `class`  
 **Main** メソッドを含む型です。  
 指定するクラス名は完全に修飾する必要があります。クラスを含む完全な名前空間を指定し、そのあとにクラス名を続ける必要があります。 たとえば、`Main` メソッドが、`MyApplication.Core` 名前空間の `Program` クラス内に置かれている場合、コンパイラ オプションは `-main:MyApplication.Core.Program` とする必要があります。

## <a name="remarks"></a>Remarks

[Main](../../programming-guide/main-and-command-args/index.md) メソッドを使用した型がコンパイル対象に 2 つ以上含まれている場合には、プログラムへのエントリ ポイントとして使用する **Main** メソッドがどの型に含まれているかを指定できます。

このオプションは、 *.exe* ファイルをコンパイルするときに使用されます。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 開発環境でこのコンパイラ オプションを設定するには

1. プロジェクトの **[プロパティ]** ページを開きます。

2. **[アプリケーション]** プロパティ ページをクリックします。

3. **[スタートアップ オブジェクト]** プロパティを変更します。

    このコンパイラ オプションをプログラムによって設定するには、「<xref:VSLangProj80.ProjectProperties3.StartupObject%2A>」を参照してください。

### <a name="to-set-this-compiler-option-by-manually-editing-the-csproj-file"></a>*.csproj* ファイルを手動で編集してこのコンパイラ オプションを設定するには

.csproj ファイルを編集し、`PropertyGroup` セクション内に `StartupObject` 要素を追加することで、このオプションを設定できます。 次に例を示します。

```xml
  <PropertyGroup>
    ...
    <StartupObject>MyApplication.Core.Program</StartupObject>
  </PropertyGroup>
```

## <a name="example"></a>例

**Main** メソッドが`Test2` にあることを指定して、`t2.cs` と `t3.cs` をコンパイルします。

```console
csc t2.cs t3.cs -main:Test2
```

## <a name="see-also"></a>関連項目

- [C# コンパイラ オプション](./index.md)
- [プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)
