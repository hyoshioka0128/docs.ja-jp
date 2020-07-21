---
title: .NET Core プロジェクト SDK の概要
titleSuffix: ''
description: .NET Core プロジェクト SDK について説明します。
ms.date: 02/02/2020
ms.topic: conceptual
ms.openlocfilehash: 9db62ab7774e3dd71412fa346d78ae0c62a2f81f
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803042"
---
# <a name="net-core-project-sdks"></a>.NET Core プロジェクト SDK

.NET Core プロジェクトは、ソフトウェア開発キット (SDK) に関連付けられています。 各 "*プロジェクト SDK*" は、MSBuild [ターゲット](/visualstudio/msbuild/msbuild-targets)と、コードのコンパイル、パッキング、発行を行う関連する[タスク](/visualstudio/msbuild/msbuild-tasks)のセットです。 プロジェクト SDK を参照するプロジェクトは、"*SDK スタイルのプロジェクト*" と呼ばれることもあります。

## <a name="available-sdks"></a>使用可能な SDK

.NET Core では、次の SDK を利用できます。

| ID | 説明 | リポジトリ|
| - | - | - |
| `Microsoft.NET.Sdk` | .NET Core SDK | <https://github.com/dotnet/sdk> |
| `Microsoft.NET.Sdk.Web` | .NET Core [Web SDK](/aspnet/core/razor-pages/web-sdk) | <https://github.com/aspnet/websdk> |
| `Microsoft.NET.Sdk.Razor` | .NET Core [Razor SDK](/aspnet/core/razor-pages/sdk) |
| `Microsoft.NET.Sdk.Worker` | .NET Core Worker Service SDK |
| `Microsoft.NET.Sdk.WindowsDesktop` | .NET Core WinForms と WPF SDK |

.NET Core SDK は、.NET Core の基本 SDK です。 他の SDK から .NET Core SDK が参照され、他の SDK に関連付けられているプロジェクトで、すべての .NET Core SDK プロパティが使用可能になります。 たとえば、Web SDK は、.NET Core SDK と Razor SDK の両方に依存しています。

NuGet を使用して配布できる独自の SDK を作成することもできます。

## <a name="project-files"></a>プロジェクト ファイル

.NET Core プロジェクトは、[MSBuild](/visualstudio/msbuild/msbuild) 形式に基づいています。 プロジェクト ファイルは、C# プロジェクトでは *.csproj*、F# プロジェクトでは *.fsproj* のような拡張子が付いていて、XML 形式です。 MSBuild プロジェクト ファイルのルート要素は、[Project](/visualstudio/msbuild/project-element-msbuild) 要素です。 `Project` 要素には、使用する SDK (およびバージョン) を指定する省略可能な `Sdk` 属性があります。 .NET Core ツールを使用してコードをビルドするには、`Sdk` 属性を、「[使用可能な SDK](#available-sdks)」の表にあるいずれかの ID に設定します。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  ...
</Project>
```

NuGet から取得した SDK を指定するには、名前の末尾にバージョンを含めるか、*global.json* ファイルに名前とバージョンを指定します。

```xml
<Project Sdk="MSBuild.Sdk.Extras/2.0.54">
  ...
</Project>
```

SDK を指定する別の方法として、トップレベルの [SDK](/visualstudio/msbuild/sdk-element-msbuild) 要素を使用する方法があります。

```xml
<Project>
  <Sdk Name="Microsoft.NET.Sdk" />
  ...
</Project>
```

これらの方法のいずれかで SDK を参照すると、.NET Core のプロジェクト ファイルが大幅に簡素化されます。 プロジェクトの評価中に、MSBuild によってプロジェクト ファイルの先頭に `Sdk.props` の暗黙的なインポートと、末尾に `Sdk.targets` の暗黙的なインポートが追加されます。

```xml
<Project>
  <!-- Implicit top import -->
  <Import Project="Sdk.props" Sdk="Microsoft.NET.Sdk" />
  ...
  <!-- Implicit bottom import -->
  <Import Project="Sdk.targets" Sdk="Microsoft.NET.Sdk" />
</Project>
```

> [!TIP]
> Windows コンピューターでは、*Sdk.props* ファイルと *Sdk.targets* ファイルは *%ProgramFiles%\dotnet\sdk\\[バージョン]\Sdks\Microsoft.NET.Sdk\Sdk* フォルダーにあります。

### <a name="preprocess-the-project-file"></a>プロジェクト ファイルの前処理

MSBuild では、`dotnet msbuild -preprocess` コマンドを使用して、SDK とそのターゲットが取り込まれた後の完全に展開されたプロジェクトがどのようになるかを確認できます。 [`dotnet msbuild`](../tools/dotnet-msbuild.md) コマンドの [preprocess](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) スイッチによって、インポートされるファイル、そのソース、ビルドに対するそのコントリビューションが、実際にプロジェクトをビルドすることなく、表示されます。

プロジェクトにターゲット フレームワークが複数存在する場合は、1 つのフレームワークだけにコマンドの結果を集中させてください。そのためには、そのフレームワークを MSBuild プロパティとして指定します。 次に例を示します。

`dotnet msbuild -property:TargetFramework=netcoreapp2.0 -preprocess:output.xml`

### <a name="default-compilation-includes"></a>コンパイルへの既定の組み込み

コンパイル項目、埋め込みリソース、および `None` 項目の既定の組み込みと除外が SDK で定義されています。 SDK 以外の .NET Framework プロジェクトとは異なり、既定値がほとんどの一般的なユース ケースに対応しているため、これらの項目をプロジェクト ファイルで指定する必要はありません。 これにより、プロジェクト ファイルのサイズがより小さく、より簡単に理解できるようになり、必要に応じて手作業で編集できます。

次の表は、.NET Core SDK に組み込まれる、および除外される要素と [glob](https://en.wikipedia.org/wiki/Glob_(programming)) の一覧を示します。

| 要素           | 含まれる glob                              | 除外される glob                                                  | glob の削除              |
|-------------------|-------------------------------------------|---------------------------------------------------------------|--------------------------|
| Compile           | \*\*/\*.cs (または他の言語拡張機能) | \*\*/\*.user;  \*\*/\*.\*proj;  \*\*/\*.sln;  \*\*/\*.vssscc  | N/A                      |
| EmbeddedResource  | \*\*/\*.resx                              | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | N/A                      |
| None              | \*\*/\*                                   | \*\*/\*.user; \*\*/\*.\*proj; \*\*/\*.sln; \*\*/\*.vssscc     | \*\*/\*.cs; \*\*/\*.resx |

> [!NOTE]
> `./bin` フォルダーと `./obj` フォルダーは、`$(BaseOutputPath)` と `$(BaseIntermediateOutputPath)` の MSBuild プロパティによって表され、既定で glob から除外されます。 除外は `$(DefaultItemExcludes)` プロパティによって表されます。

#### <a name="build-errors"></a>ビルド エラー

これらの項目をプロジェクト ファイルに明示的に定義すると、次のような "NETSDK1022" ビルド エラーが発生する可能性があります。

  > 重複する 'Compile' 項目が含まれていました。 .NET SDK には、既定でプロジェクト ディレクトリの 'Compile' 項目が含まれています。 これらの項目をプロジェクト ファイルから削除するか、プロジェクト ファイルに明示的に含める場合は 'EnableDefaultCompileItems' プロパティを 'false' に設定することができます。

  > 重複する 'EmbeddedResource' 項目が含まれていました。 .NET SDK には、既定でプロジェクト ディレクトリの 'EmbeddedResource' 項目が含まれています。 これらの項目をプロジェクト ファイルから削除するか、プロジェクト ファイルに明示的に含める場合は 'EnableDefaultEmbeddedResourceItems' プロパティを 'false' に設定することができます。

このエラーを解決するには、次のいずれかの操作を行います。

- 前の表に列挙されている暗黙的な項目と一致する明示的な `Compile`、`EmbeddedResource`、または `None` の項目を削除します。

- 次のように `EnableDefaultItems` プロパティを `false` に設定して、暗黙的なファイルの組み込みをすべて無効にします。

  ```xml
  <PropertyGroup>
    <EnableDefaultItems>false</EnableDefaultItems>
  </PropertyGroup>
  ```

  アプリで発行する一部のファイルを指定する必要がある場合は、そのために既知の MSBuild のしくみ (たとえば `Content` 要素) を引き続き使用できます。

- `EnableDefaultCompileItems`、`EnableDefaultEmbeddedResourceItems`、または `EnableDefaultNoneItems` プロパティを `false` に設定することによって、`Compile`、`EmbeddedResource`、または `None` glob のみを選択的に無効にします。

  ```xml
  <PropertyGroup>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
    <EnableDefaultEmbeddedResourceItems>false</EnableDefaultEmbeddedResourceItems>
    <EnableDefaultNoneItems>false</EnableDefaultNoneItems>
  </PropertyGroup>
  ```

  `Compile` glob のみを無効にすると、Visual Studio のソリューション エクスプローラーに \*.cs 項目がプロジェクトの一部として (`None` 項目として組み込まれて) 引き続き表示されます。 暗黙的な `None` glob を無効にするには、`EnableDefaultNoneItems` も `false` に設定します。

## <a name="customize-the-build"></a>ビルドのカスタマイズ

[ビルドをカスタマイズする](/visualstudio/msbuild/customize-your-build)には、さまざまな方法があります。 プロパティを引数として [msbuild](/visualstudio/msbuild/msbuild-command-line-reference) または [dotnet](../tools/index.md) コマンドに渡すことによって、プロパティをオーバーライドすることができます。 また、プロパティをプロジェクト ファイルに追加することや、*Directory.Build.props* ファイルに追加することができます。 .NET Core プロジェクトの便利なプロパティの一覧については、「[.NET Core SDK プロジェクトの MSBuild リファレンス](msbuild-props.md)」を参照してください。

### <a name="custom-targets"></a>カスタム ターゲット

.NET Core プロジェクトでは、プロジェクトで使用するカスタムの MSBuild ターゲットとプロパティをパッケージ化し、そのパッケージをプロジェクトで使用することができます。 この種の拡張機能を使用するのは、次の場合です。

- ビルド処理を拡張する。
- ビルド プロセスの成果物 (生成されたファイルなど) にアクセスする。
- どのような構成でビルドが呼び出されるかを検査する。

カスタムのビルド ターゲットまたはプロパティを追加するには、プロジェクトの *build* フォルダーに `<package_id>.targets` または `<package_id>.props` の形式のファイル (たとえば `Contoso.Utility.UsefulStuff.targets`) を配置します。

次の XML は *.csproj* ファイルからのスニペットです。パッケージ化する対象を [`dotnet pack`](../tools/dotnet-pack.md) コマンドに指示しています。 `<ItemGroup Label="dotnet pack instructions">` 要素で、パッケージ内の *build* フォルダーにターゲット ファイルを配置します。 `<Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">` 要素で、アセンブリと *.json* ファイルを *build* フォルダーに配置します。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  ...
  <ItemGroup Label="dotnet pack instructions">
    <Content Include="build\*.targets">
      <Pack>true</Pack>
      <PackagePath>build\</PackagePath>
    </Content>
  </ItemGroup>
  <Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">
    <!-- Collect these items inside a target that runs after build but before packaging. -->
    <ItemGroup>
      <Content Include="$(OutputPath)\*.dll;$(OutputPath)\*.json">
        <Pack>true</Pack>
        <PackagePath>build\</PackagePath>
      </Content>
    </ItemGroup>
  </Target>
  ...
  
</Project>
```

プロジェクトでカスタム ターゲットを使用するには、パッケージとそのバージョンを指す `PackageReference` 要素を追加します。 ツールとは異なり、カスタム ターゲットのパッケージは、それを使用するプロジェクトの依存関係クロージャに含まれます。

カスタム ターゲットの使用方法を構成できます。 それは MSBuild ターゲットであるため、指定されたターゲットに依存することや、別のターゲットの後に実行したり、`dotnet msbuild -t:<target-name>` コマンドを使用して手動で呼び出したりすることができます。 ただし、優れたユーザー エクスペリエンスを提供するために、プロジェクトごとのツールとカスタム ターゲットを組み合わせることができます。 このシナリオでは、必要なすべてのパラメーターをプロジェクトごとのツールで受け取り、受け取ったパラメーターを、ターゲットを実行する必要な [`dotnet msbuild`](../tools/dotnet-msbuild.md) の呼び出しに変換します。 このような相乗効果のサンプルは、[`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer) プロジェクトの「[MVP Summit 2016 Hackathon samples](https://github.com/dotnet/MVPSummitHackathon2016)」 (MVP Summit 2016 ハッカソンのサンプル) レポートで参照することができます。

## <a name="see-also"></a>関連項目

- [.NET Core をインストールする](../install/index.yml)
- [MSBuild プロジェクト SDK の使用方法](/visualstudio/msbuild/how-to-use-project-sdk)
- [カスタムの MSBuild ターゲットとプロパティを NuGet でパッケージ化する](/nuget/create-packages/creating-a-package#include-msbuild-props-and-targets-in-a-package)
