---
title: SDK テンプレートのインストールと管理 - .NET Core
description: Windows、Linux、macOS に .NET Core テンプレートをインストールする方法について説明します。
author: adegeo
ms.author: adegeo
ms.date: 04/24/2020
zone_pivot_groups: operating-systems-set-one
no-loc:
- dotnet new
- dotnet nuget add source
ms.openlocfilehash: 09acae1409eb0492be10bd3a61b14da5be57c6c7
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324486"
---
# <a name="manage-net-project-and-item-templates"></a>.NET のプロジェクトと項目のテンプレートを管理する

.NET Core 付属のテンプレート システムを利用すると、NuGet、NuGet パッケージ ファイル、ファイル システム ディレクトリからテンプレートをインストールしたり、アンインストールしたりできます。 この記事では、.NET Core SDK CLI を使用して .NET Core テンプレートを管理する方法について説明します。

テンプレートの作成方法については、「[チュートリアル: テンプレートを作成する](../tutorials/cli-templates-create-item-template.md)」を参照してください。

## <a name="install-template"></a>テンプレートのインストール

テンプレートは `-i` パラメーターを指定して [dotnet new](../tools/dotnet-new.md) SDK コマンドを実行することでインストールされます。 テンプレートの NuGet パッケージ ID かテンプレート ファイルが含まれるフォルダーの NuGet パッケージ ID を指定できます。

### <a name="nuget-hosted-package"></a>NuGet でホストされるパッケージ

.NET CLI テンプレートは広範囲に配布する目的で [NuGet](https://www.nuget.org/) にアップロードされます。 テンプレートはプライベート フィードからもインストールできます。 テンプレートを NuGet フィードにアップロードする代わりに、*nupkg* テンプレート ファイルを配布し、手動でインストールできます。詳細は「[ローカル NuGet パッケージ](#local-nuget-package)」セクションにあります。

NuGet フィード構成の詳細については、「[dotnet nuget add source](../tools/dotnet-nuget-add-source.md)」を参照してください。

既定の NuGet フィードからテンプレート パックをインストールするには、`dotnet new -i {package-id}` コマンドを使用します。

```dotnetcli
dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates
```

特定のバージョンの既定の NuGet フィードからテンプレート パックをインストールするには、`dotnet new -i {package-id}::{version}` コマンドを使用します。

```dotnetcli
dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates::2.2.6
```

### <a name="local-nuget-package"></a>ローカル NuGet パッケージ

テンプレート パックが作成されると、*nupkg* ファイルが生成されます。 *nupkg* ファイルにテンプレートが含まれる場合、`dotnet new -i {path-to-package}` コマンドでそれをインストールできます。

::: zone pivot="os-windows"

```dotnetcli
dotnet new -i c:\code\nuget-packages\Some.Templates.1.0.0.nupkg
```

::: zone-end

::: zone pivot="os-linux,os-macos"

```dotnetcli
dotnet new -i ~/code/nuget-packages/Some.Templates.1.0.0.nupkg
```

::: zone-end

### <a name="folder"></a>フォルダー

*nupkg* ファイルからテンプレートをインストールする代わりに、`dotnet new -i {folder-path}` コマンドで直接、フォルダーからテンプレートをインストールすることもできます。 指定されたフォルダーは、見つかったテンプレートのテンプレート パック ID として扱われます。 指定されたフォルダーの階層で見つかったテンプレートはすべてインストールされます。

::: zone pivot="os-windows"

```dotnetcli
dotnet new -i c:\code\nuget-packages\some-folder\
```

::: zone-end

::: zone pivot="os-linux,os-macos"

```dotnetcli
dotnet new -i ~/code/nuget-packages/some-folder/
```

::: zone-end

コマンドで指定された `{folder-path}` は、見つかったすべてのコマンドのテンプレート パック ID になります。 「[テンプレート リスト](#list-templates)」セクションに指定されているとおり、インストールされているテンプレートのリストは `dotnet new -u` コマンドで取得できます。 この例では、テンプレート パック ID はインストールに使用されるフォルダーとして表示されます。

::: zone pivot="os-windows"

```console
dotnet new -u
Template Instantiation Commands for .NET Core CLI

Currently installed items:

... cut to save space ...

  c:\code\nuget-packages\some-folder
    Templates:
      A Template Console Class (templateconsole) C#
      Project for some technology (contosoproject) C#
    Uninstall Command:
      dotnet new -u c:\code\nuget-packages\some-folder
```

::: zone-end

::: zone pivot="os-linux,os-macos"

```console
dotnet new -u
Template Instantiation Commands for .NET Core CLI

Currently installed items:

... cut to save space ...

  /home/username/code/templates
    Templates:
      A Template Console Class (templateconsole) C#
      Project for some technology (contosoproject) C#
    Uninstall Command:
      dotnet new -u /home/username/code/templates
```

::: zone-end

## <a name="uninstall-template"></a>テンプレートをアンインストールする

テンプレートは `-u` パラメーターを指定して [dotnet new](../tools/dotnet-new.md) SDK コマンドを実行することでアンインストールされます。 テンプレートの NuGet パッケージ ID かテンプレート ファイルが含まれるフォルダーの NuGet パッケージ ID を指定できます。

### <a name="nuget-package"></a>NuGet パッケージ

NuGet フィードまたは *nupkg* ファイルから NuGet テンプレート パックをインストールした後、NuGet パッケージ ID を参照してアンインストールできます。

テンプレート パックをアンインストールするには、`dotnet new -u {package-id}` コマンドを使用します。

```dotnetcli
dotnet new -u Microsoft.DotNet.Web.Spa.ProjectTemplates
```

### <a name="folder"></a>フォルダー

テンプレートが[フォルダー パス](#folder)からインストールされるとき、そのフォルダー パスがテンプレート パック ID になります。

テンプレート パックをアンインストールするには、`dotnet new -u {package-folder-path}` コマンドを使用します。

::: zone pivot="os-windows"

```dotnetcli
dotnet new -u c:\code\nuget-packages\some-folder
```

::: zone-end

::: zone pivot="os-linux,os-macos"

```dotnetcli
dotnet new -u /home/username/code/templates
```

::: zone-end

## <a name="list-templates"></a>テンプレート リスト

パッケージ ID なしで標準的なアンインストール コマンドを使用することで、各テンプレートをアンインストールするコマンドと共に、インストール済みのテンプレートの一覧を表示できます。

```console
dotnet new -u
Template Instantiation Commands for .NET Core CLI

Currently installed items:

... cut to save space ...

  c:\code\nuget-packages\some-folder
    Templates:
      A Template Console Class (templateconsole) C#
      Project for some technology (contosoproject) C#
    Uninstall Command:
      dotnet new -u c:\code\nuget-packages\some-folder
```

## <a name="install-templates-from-other-sdks"></a>他の SDK からテンプレートをインストールする

SDK の各バージョンを順番にインストールしている場合、たとえば、SDK 2.0 をインストールし、次に SDK 2.1 をインストールするといった具合にインストールしている場合、各 SDK のテンプレートがインストールされています。 ただし、3.1 など、最新版の SDK から始める場合、[LTS (長期サポート) リリース](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)のテンプレートのみが含まれます。これは SDK 3.1 のリリース時点で SDK 2.1 と SDK 3.1 になります。 その他のリリースのテンプレートは含まれていません。

.NET Core テンプレートは NuGet で入手できて、他のあらゆるテンプレートと同じようにインストールできます。 詳細については、「[NuGet でホストされているパッケージをインストールする](#nuget-hosted-package)」を参照してください。

| SDK              | NuGet パッケージ ID                                                                                                      |
|------------------|-------------------------------------------------------------------------------------------------------------------------------|
| .NET Core 2.1    | [`Microsoft.DotNet.Common.ProjectTemplates.2.1`](https://www.nuget.org/packages/Microsoft.DotNet.Common.ProjectTemplates.2.1) |
| .NET Core 2.2    | [`Microsoft.DotNet.Common.ProjectTemplates.2.2`](https://www.nuget.org/packages/Microsoft.DotNet.Common.ProjectTemplates.2.2) |
| .NET Core 3.0    | [`Microsoft.DotNet.Common.ProjectTemplates.3.0`](https://www.nuget.org/packages/Microsoft.DotNet.Common.ProjectTemplates.3.0) |
| .NET Core 3.1    | [`Microsoft.DotNet.Common.ProjectTemplates.3.1`](https://www.nuget.org/packages/Microsoft.DotNet.Common.ProjectTemplates.3.1) |
| ASP.NET Core 2.1 | [`Microsoft.DotNet.Web.ProjectTemplates.2.1`](https://www.nuget.org/packages/Microsoft.DotNet.Web.ProjectTemplates.2.1)       |
| ASP.NET Core 2.2 | [`Microsoft.DotNet.Web.ProjectTemplates.2.2`](https://www.nuget.org/packages/Microsoft.DotNet.Web.ProjectTemplates.2.2)       |
| ASP.NET Core 3.0 | [`Microsoft.DotNet.Web.ProjectTemplates.3.0`](https://www.nuget.org/packages/Microsoft.DotNet.Web.ProjectTemplates.3.0)       |
| ASP.NET Core 3.1 | [`Microsoft.DotNet.Web.ProjectTemplates.3.1`](https://www.nuget.org/packages/Microsoft.DotNet.Web.ProjectTemplates.3.1)       |

たとえば、.NET Core SDK には .NET Core 2.1 と .NET Core 3.1 を対象とするコンソール アプリ向けのテンプレートが含まれています。 .NET Core 3.0 を対象にする場合、3.0 テンプレートをインストールする必要があるかもしれません。

01. .NET Core 3.0 を対象とするアプリを作成してみてください。

    ```dotnetcli
    dotnet new console --framework netcoreapp3.0
    ```

    エラー メッセージが表示された場合、テンプレートをインストールする必要があります。

    > 入力内容と一致するインストール済みテンプレートが見つかりません。オンラインで検索してください...

01. .NET Core 3.0 プロジェクト テンプレートをインストールします。

    ```dotnetcli
    dotnet new -i Microsoft.DotNet.Common.ProjectTemplates.3.0
    ```

01. アプリをもう一度作成してみてください。

    ```dotnetcli
    dotnet new console --framework netcoreapp3.0
    ```

    プロジェクトが作成されたことを示すメッセージが表示されるはずです。

    > テンプレート "Console Application" が正常に作成されました。
    >
    > 作成後のアクションを処理しています...path-to-project-file.csproj で "dotnet restore" を実行しています...復元対象のプロジェクトを決定しています...path-to-project-file.csproj の復元は 1.05 秒後に完了します。
    >
    > 正常に復元されました。

## <a name="see-also"></a>関連項目

- [チュートリアル: 項目テンプレートを作成する](../tutorials/cli-templates-create-item-template.md)
- [dotnet new](../tools/dotnet-new.md)
- [dotnet nuget add source](../tools/dotnet-nuget-add-source.md)
