---
title: .NET Core 3.0 の新機能
description: .NET Core 3.0 の新機能について説明します。
dev_langs:
- csharp
- vb
author: thraka
ms.author: adegeo
ms.date: 09/22/2019
ms.openlocfilehash: ddb758b942099657708e79b590c7817c309396d7
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216263"
---
# <a name="whats-new-in-net-core-30"></a>.NET Core 3.0 の新機能

この記事では、.NET Core 3.0 の新機能について説明します。 最も大きな強化点の 1 つは、Windows デスクトップ アプリケーションのサポートです (Windows のみ)。 .NET Core 3.0 SDK コンポーネントの Windows デスクトップを使用して、Windows フォームおよび Windows Presentation Foundation (WPF) アプリケーションを移植することができます。 誤解のないように言うと、Windows Desktop コンポーネントは Windows でのみサポートされており、Windows にのみ含まれています。 詳細については、この記事で後述する「[Windows デスクトップ](#windows-desktop)」を参照してください。

.NET Core 3.0 では C# 8.0 のサポートが追加されています。 **C# の拡張機能**では、[Visual Studio 2019 16.3](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)、[Visual Studio for Mac 8.3](/visualstudio/mac/install-preview)、または [Visual Studio Code](https://code.visualstudio.com/) を使用することを強くお勧めします。

[.NET Core 3.0 を今すぐダウンロード](https://aka.ms/netcore3download)して Windows、macOS、または Linux 上で使い始めましょう。

リリースの詳細については、[.NET Core 3.0 のアナウンス](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-0/)を参照してください。

.NET Core RC1 は、運用の準備ができていると Microsoft で見なされていたもので、完全にサポートされていました。 プレビュー リリースを使用している場合は、サポートを継続するために RTM バージョンに移行する必要があります。

## <a name="net-core-sdk-windows-installer"></a>.NET Core SDK Windows インストーラー

Windows 用の MSI インストーラーは、.NET Core 3.0 から変更されました。 SDK インストーラーは、SDK 機能帯リリースのアップグレードを実行するようになります。 機能帯は、バージョン番号の "*パッチ*" セクションの *100* 番台のグループで定義されます。 たとえば、**3.0._101_** と **3.0._201_** は 2 つの異なる機能帯のバージョンですが、**3.0._101_** と **3.0._199_** は同じ機能帯に含まれます。 また、.NET Core SDK **3.0._101_** をインストールすると、.NET Core SDK **3.0._100_** が存在する場合はマシンから削除されます。 同じマシンに .NET Core SDK **3.0._200_** をインストールすると、.NET Core SDK **3.0._101_** は削除されません。

バージョン管理の詳細については、「[.NET Core をバージョン管理する方法の概要](../versions/index.md)」を参照してください。

## <a name="c-80"></a>C# 8.0

C#8.0 も、このリリースの一部であり、null を許容する参照型の機能、非同期ストリーム、追加のパターンが含まれます。 C# 8.0 の機能の詳細については、「[C# 8.0 の新機能](../../csharp/whats-new/csharp-8.md)」を参照してください。

## <a name="net-standard-21"></a>.NET Standard 2.1

.NET Core 3.0 は **.NET Standard 2.1** をサポートしていますが、既定の `dotnet new classlib` テンプレートでは、引き続き **.NET Standard 2.0** をターゲットとするプロジェクトが生成されます。 **.NET Standard 2.1** をターゲットにするには、プロジェクト ファイルを編集して `TargetFramework` プロパティを `netstandard2.1` に変更します。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.1</TargetFramework>
  </PropertyGroup>

</Project>
```

Visual Studio を使用している場合、Visual Studio 2017 では **.NET Standard 2.1** または **.NET Core 3.0** がサポートされていないため、[Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) が必要です。

## <a name="improved-net-core-version-apis"></a>強化された .NET Core バージョン API

.NET Core 3.0 以降、.NET Core に提供されているバージョン API から、期待どおりの情報が返されるようになりました。 次に例を示します。

```csharp
System.Console.WriteLine($"Environment.Version: {System.Environment.Version}");

// Old result
//   Environment.Version: 4.0.30319.42000
//
// New result
//   Environment.Version: 3.0.0
```

```csharp
System.Console.WriteLine($"RuntimeInformation.FrameworkDescription: {System.Runtime.InteropServices.RuntimeInformation.FrameworkDescription}");

// Old result
//   RuntimeInformation.FrameworkDescription: .NET Core 4.6.27415.71
//
// New result
//   RuntimeInformation.FrameworkDescription: .NET Core 3.0.0-preview4-27615-11
```

> [!WARNING]
> 破壊的変更。 バージョン管理スキームが変更されたので、これは技術的には破壊的変更です。

## <a name="net-platform-dependent-intrinsics"></a>.NET プラットフォーム依存性

特定のパフォーマンス指向 CPU 命令 (**SIMD** や **ビット操作命令**セット) にアクセスできるようにする API が追加されました。 これらの命令は、データを並列で効率的に処理するといった、特定のシナリオでパフォーマンスを大幅に向上するのに役立ちます。

.NET ライブラリでは、必要に応じて、パフォーマンスを向上するためにこれらの命令が使用されるようになりました。

詳細については、「[.NET Platform Dependent Intrinsics (.NET プラットフォーム依存性)](https://github.com/dotnet/designs/blob/master/accepted/platform-intrinsics.md)」を参照してください。

## <a name="default-executables"></a>既定の実行可能ファイル

.NET Core では、既定で[フレームワーク依存の実行可能ファイル](../deploying/index.md#framework-dependent-executables-fde)が作成されるようになりました。 この動作は、グローバルにインストールされているバージョンの .NET Core を使用するアプリケーションの新機能です。 以前は、[自己完結型の配置](../deploying/index.md#self-contained-deployments-scd)でのみ実行可能ファイルが生成されました。

`dotnet build` または `dotnet publish` の実行中に、使用している SDK の環境およびプラットフォームと一致する実行可能ファイルが作成されます。 これらの実行可能ファイルでは、次のような他のネイティブ実行可能ファイルと同じことを期待できます。

- 実行可能ファイルはダブルクリックすることができます。
- Windows では `myapp.exe`、Linux と macOS では`./myapp` など、コマンド プロンプトからアプリケーションを直接起動できます。

## <a name="single-file-executables"></a>単一ファイルの実行可能ファイル

`dotnet publish` コマンドは、プラットフォーム固有の単一ファイルの実行可能ファイルにアプリをパッケージ化することをサポートします。 実行可能ファイルは自己展開型であり、アプリの実行に必要なすべての依存関係 (ネイティブを含む) が含まれます。 アプリを初めて実行すると、アプリ名とビルド ID に基づいてアプリケーションがディレクトリに抽出されます。 アプリケーションを再実行すると、起動は速くなります。 新しいバージョンが使用されない限り、アプリケーションは自身を 2 回抽出する必要がありません。

単一ファイルの実行可能ファイルを発行するには、プロジェクト内またはコマンド ラインで `dotnet publish` コマンドを使用して `PublishSingleFile` を設定します。

```xml
<PropertyGroup>
  <RuntimeIdentifier>win10-x64</RuntimeIdentifier>
  <PublishSingleFile>true</PublishSingleFile>
</PropertyGroup>
```

または

```dotnetcli
dotnet publish -r win10-x64 /p:PublishSingleFile=true
```

単一ファイルの発行の詳細については、[単一ファイル バンドラー設計のドキュメント](https://github.com/dotnet/designs/blob/master/accepted/single-file/design.md)を参照してください。

## <a name="assembly-linking"></a>アセンブリのリンク

.NET Core 3.0 SDK に付属するツールを使うと、IL を分析し、未使用のアセンブリをトリミングすることによって、アプリのサイズを減らすことができます。

自己完結型アプリには、コードの実行に必要なものがすべて含まれるので、ホスト コンピューターに .NET をインストールする必要はありません。 ただし、多くの場合、アプリが機能するにはフレームワークの小さなサブセットのみが必要であり、使用されていない他のライブラリは削除できます。

.NET Core には、[IL リンカー](https://github.com/mono/linker) ツールを使ってアプリの IL をスキャンする設定が含まれるようになっています。 このツールでは、必要なコードが検出された後、使われていないライブラリがトリミングされます。 このツールを使うと、一部のアプリの展開サイズを大幅に削減できます。

このツールを有効にするには、プロジェクトで `<PublishTrimmed>` 設定を追加し、自己完結型アプリを発行します。

```xml
<PropertyGroup>
  <PublishTrimmed>true</PublishTrimmed>
</PropertyGroup>
```

```dotnetcli
dotnet publish -r <rid> -c Release
```

たとえば、含まれている基本的な "hello world" という新しいコンソール プロジェクト テンプレートは、発行されるときに、サイズが約 70 MB になります。 `<PublishTrimmed>` を使うことにより、そのサイズが約 30 MB に減ります。

考慮すべき重要なこととして、リフレクションまたは関連する動的機能を使っているアプリケーションまたはフレームワーク (ASP.NET Core と WPF を含む) では、トリミングすると壊れることがよくあります。 このような破損が発生するのは、リンカーはこの動的な動作を認識しておらず、リフレクションに必要なフレームワークの種類を判断できないためです。 IL リンカー ツールは、このシナリオを認識するように構成できます。

何よりも、必ずトリミング後のアプリをテストしてください。

IL リンカー ツールについて詳しくは、[ドキュメント](https://aka.ms/dotnet-illink)または [mono/linker]( https://github.com/mono/linker) リポジトリをご覧ください。

## <a name="tiered-compilation"></a>階層型コンパイル

.NET Core 3.0 では、[階層型コンパイル](https://devblogs.microsoft.com/dotnet/tiered-compilation-preview-in-net-core-2-1/) (TC) が既定で有効になりました。 この機能により、ランタイムが状況に応じて Just-In-Time (JIT) コンパイラを使用してパフォーマンスを向上できるようになりました。

TC の主な利点は、低品質で高速な階層または高品質で低速な階層を使った (再) JIT メソッドが可能になることです。 これは、起動から安定した状態まで、さまざまな実行段階を経るときに、アプリケーションのパフォーマンスを向上するために役立ちます。 これは、すべてのメソッドが 1 つの方法 (高品質階層と同じ) でコンパイルされ、起動時のパフォーマンスよりも安定した状態に偏っている非 TC アプローチとは対照的です。

Quick JIT (階層 0 の JIT 済みコード) を有効にするには、プロジェクト ファイルで次の設定を使用します。

```xml
<PropertyGroup>
  <TieredCompilationQuickJit>true</TieredCompilationQuickJit>
</PropertyGroup>
```

TC を完全に無効にするには、プロジェクト ファイルでこの設定を使用します。

```xml
<TieredCompilation>false</TieredCompilation>
```

## <a name="readytorun-images"></a>ReadyToRun イメージ

アプリケーション アセンブリを ReadyToRun (R2R) 形式としてコンパイルすることで、.NET Core アプリケーションの起動時間を向上させることができます。 R2R とは、Ahead-Of-Time (AOT) コンパイルの一種です。

R2R バイナリでは、アプリケーションの読み込み時に Just-In-Time (JIT) コンパイラで行う必要がある作業量を減らすことにより、起動時のパフォーマンスが向上します。 バイナリには、JIT で生成されるものと似たネイティブ コードが含まれます。 ただし、R2R バイナリは、中間言語 (IL) コード (一部のシナリオでまだ必要です) と同じコードのネイティブ バージョンの両方が含まれるため、大きくなります。 R2R は、Linux x64 や Windows x64 などの特定のランタイム環境 (RID) をターゲットとする自己完結型アプリを発行するときにのみ使用できます。

ReadyToRun としてプロジェクトをコンパイルするには、次の手順を行います。

01. `<PublishReadyToRun>` 設定をプロジェクトに追加します。

    ```xml
    <PropertyGroup>
      <PublishReadyToRun>true</PublishReadyToRun>
    </PropertyGroup>
    ```

01. 自己完結型アプリを発行します。 たとえば、次のコマンドでは、Windows の 64 ビット版向けの自己完結型アプリが作成されます。

    ```dotnetcli
    dotnet publish -c Release -r win-x64 --self-contained true
    ```

### <a name="cross-platformarchitecture-restrictions"></a>クロス プラットフォーム/アーキテクチャの制限

現在、ReadyToRun コンパイラではクロスターゲットはサポートされていません。 特定のターゲットに対してコンパイルする必要があります。 たとえば、Windows x64 用の R2R イメージが必要な場合は、その環境で publish コマンドを実行する必要があります。

クロスターゲットに対する例外:

- Windows x64 を使って、Windows ARM32、ARM64、x86 のイメージをコンパイルできます。
- Windows x86 を使って、Windows ARM32 のイメージをコンパイルできます。
- Linux x64 を使って、Linux ARM32 と ARM64 のイメージをコンパイルできます。

## <a name="build-copies-dependencies"></a>ビルドによる依存関係のコピー

`dotnet build` コマンドでは、アプリケーションの NuGet 依存関係が NuGet キャッシュからビルド出力フォルダーにコピーされるようになりました。 以前は、依存関係のコピーは `dotnet publish` の一部としてのみ行われていました。

リンクや razor ページの発行など、まだ発行が必要な操作がいくつかあります。

## <a name="local-tools"></a>ローカル ツール

.NET Core 3.0 にローカル ツールが導入されました。 ローカル ツールは[グローバル ツール](../tools/global-tools.md)に似ていますが、ディスク上の特定の場所に関連付けられています。 ローカル ツールはグローバルには使用できず、NuGet パッケージとして配布されます。

> [!WARNING]
> .NET Core 3.0 Preview 1 で `dotnet tool restore` や `dotnet tool install` の実行などのローカル ツールを試した場合は、ローカル ツールのキャッシュ フォルダーを削除します。 そうしないと、ローカル ツールは新しいリリースで動作しません。 このフォルダーは次の場所にあります。
>
> macOS、Linux の場合: `rm -r $HOME/.dotnet/toolResolverCache`
>
> Windows の場合: `rmdir /s %USERPROFILE%\.dotnet\toolResolverCache`

ローカル ツールは、現在のディレクトリ内のマニフェスト ファイル名 `dotnet-tools.json` に依存しています。 このマニフェスト ファイルは、ツールをそのフォルダー下で使用できるように定義します。 コードを使用するすべての人が確実に同じツールを復元して使用できるように、自分のコードと一緒にマニフェスト ファイルを配布することができます。

グローバル ツールとローカル ツールの両方で、ランタイムの互換バージョンが必要です。 現在 NuGet.org 上にある多くのツールは、.NET Core Runtime 2.1 をターゲットとしています。 グローバルにまたはローカルにこのようなツールをインストールするには、[NET Core 2.1 ランタイム](https://dotnet.microsoft.com/download/dotnet-core/2.1)をインストールする必要があります。

## <a name="major-version-roll-forward"></a>メジャーバージョンのロールフォワード

.NET Core 3.0 では、アプリを最新メジャー バージョンの .NET Core にロールフォワードできるようにするオプトイン機能が導入されました。 さらに、ロールフォワードをアプリに適用する方法を制御する新しい設定が追加されました。 これは、以下の方法で構成できます。

- プロジェクト ファイルのプロパティ: `RollForward`
- ランタイム構成ファイルのプロパティ: `rollForward`
- 環境変数: `DOTNET_ROLL_FORWARD`
- コマンドライン引数: `--roll-forward`

次の値のいずれかを指定する必要があります。 設定を省略すると、**Minor** が既定値になります。

- **LatestPatch**\
最新のパッチ バージョンにロールフォワードします。 これで、マイナー バージョンのロールフォワードが無効になります。
- **Minor**\
要求されたマイナー バージョンが見つからない場合は、それよりも高い最小マイナー バージョンにロールフォワードします。 要求されたマイナー バージョンが存在する場合は、**LatestPatch** ポリシーが使用されます。
- **Major**\
要求されたメジャー バージョンが見つからない場合は、それよりも高い最小メジャー バージョンで最小マイナー バージョンにロールフォワードします。 要求されたメジャー バージョンが存在する場合は、**Minor** ポリシーが使用されます。
- **LatestMinor**\
要求されたマイナー バージョンが存在する場合でも、最上位のマイナー バージョンにロールフォワードします。 コンポーネント ホスティング シナリオを対象としています。
- **LatestMajor**\
要求されたメジャーが存在する場合でも、最上位のメジャー バージョンで最上位のマイナー バージョンにロールフォワードします。 コンポーネント ホスティング シナリオを対象としています。
- **Disable**\
ロールフォワードしません。 指定されたバージョンにのみバインドします。 このポリシーは、最新のパッチにロールフォワードする機能が無効になるため、一般的な使用にはお勧めできません。 この値はテスト用にのみ推奨されます。

**Disable** の設定を除くすべての設定では、利用できる最新のパッチ バージョンが使用されます。

## <a name="windows-desktop"></a>Windows デスクトップ

.NET Core 3.0 は、Windows Presentation Foundation (WPF) および Windows フォームを使用した Windows デスクトップ アプリケーションをサポートしています。 これらのフレームワークでは、Windows UI XAML ライブラリ (WinUI) の最新のコントロールと Fluent スタイルを [XAML Islands](/windows/uwp/xaml-platform/xaml-host-controls) 経由で使用することもできます。

Windows デスクトップ コンポーネントは、Windows .NET Core 3.0 SDK の一部です。

次の `dotnet` コマンドを使用して、新しい WPF または Windows フォーム アプリケーションを作成できます。

```dotnetcli
dotnet new wpf
dotnet new winforms
```

Visual Studio 2019 では、.NET Core 3.0 Windows フォームと WPF 用に、**新しいプロジェクト** テンプレートが追加されました。

既存の .NET Framework アプリケーションを移植する方法の詳細については、[WPF プロジェクトの移植](../porting/wpf.md)と [Windows フォーム プロジェクトの移植](../porting/winforms.md)に関する記事を参照してください。

## <a name="com-callable-components---windows-desktop"></a>COM 呼び出し可能コンポーネント - Windows デスクトップ

Windows 上で、COM 呼び出し可能なマネージ コンポーネントを作成できるようになりました。 この機能は、COM アドイン モデルに .NET Core を使用する場合と、.NET Framework にパリティを提供する場合にも重要です。

COM サーバーとして *mscoree.dll* が使用されていた .NET Framework とは異なり、COM コンポーネントを構築すると、.NET Core によって *bin* ディレクトリにネイティブ ランチャー DLL が追加されます。

COM コンポーネントを作成して使用する方法の例については、[COM のデモ](https://github.com/dotnet/samples/tree/master/core/extensions/COMServerDemo)に関する記事を参照してください。

## <a name="msix-deployment---windows-desktop"></a>MSIX の展開 - Windows デスクトップ

[MSIX](https://docs.microsoft.com/windows/msix/) は新しい Windows アプリケーション パッケージ形式です。 これは、Windows 10 に .NET Core 3.0 のデスクトップ アプリケーションを展開するために使用できます。

[Windows アプリケーション パッケージ プロジェクト](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-packaging-dot-net)は、Visual Studio 2019 で使用でき、[自己完結型](../deploying/index.md#self-contained-deployments-scd)の .NET Core アプリケーションを使用して、MSIX パッケージを作成することができます。

.NET Core プロジェクト ファイルの `<RuntimeIdentifiers>` プロパティで、サポートされているランタイムを指定する必要があります。

```xml
<RuntimeIdentifiers>win-x86;win-x64</RuntimeIdentifiers>
```

## <a name="winforms-high-dpi"></a>WinForms の高 DPI

.NET Core Windows フォーム アプリケーションでは、<xref:System.Windows.Forms.Application.SetHighDpiMode(System.Windows.Forms.HighDpiMode)?displayProperty=nameWithType> を使用して高 DPI モードを設定できます。 `Application.Run` の前の `App.Manifest` や P/Invoke などの他の方法で設定を指定しない限り、`SetHighDpiMode` メソッドによって、対応する高 DPI モードが設定されます。

<xref:System.Windows.Forms.HighDpiMode?displayProperty=nameWithType> 列挙型で表される `highDpiMode` に使用できる値は次のとおりです。

- `DpiUnaware`
- `SystemAware`
- `PerMonitor`
- `PerMonitorV2`
- `DpiUnawareGdiScaled`

高 DPI モードの詳細については、「[Windows での高 DPI デスクトップ アプリケーション開発](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)」をご覧ください。

## <a name="ranges-and-indices"></a>範囲とインデックス

新しい <xref:System.Index?displayProperty=nameWithType> 型はインデックス作成に使用できます。 先頭からカウントする `int` か、末尾からカウントするプレフィックス `^` 演算子 (C#) を使用して作成することができます。

```csharp
Index i1 = 3;  // number 3 from beginning
Index i2 = ^4; // number 4 from end
int[] a = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
Console.WriteLine($"{a[i1]}, {a[i2]}"); // "3, 6"
```

また、<xref:System.Range?displayProperty=nameWithType> 型もあります。これは開始値と終了値の 2 つの `Index` 値から構成され、`x..y` の範囲式 (C#) で記述できます。 これで、`Range` を使用してインデックスを付け、スライスを生成することができます。

```csharp
var slice = a[i1..i2]; // { 3, 4, 5 }
```

詳細については、[範囲とインデックスのチュートリアル](../../csharp/tutorials/ranges-indexes.md)を参照してください。

## <a name="async-streams"></a>非同期ストリーム

<xref:System.Collections.Generic.IAsyncEnumerable%601> 型は、<xref:System.Collections.Generic.IEnumerable%601> の新しい非同期バージョンです。 この言語では、その要素を使用するために `IAsyncEnumerable<T>` よりも `await foreach` を行い、要素を生成するために `yield return` を使用することができます。

非同期ストリームの生成の両方の使用例を次に示します。 `foreach` ステートメントは非同期であり、`yield return` を使用して呼び出し元の非同期ストリームを生成します。 (`yield return` を使用する) このパターンは、非同期ストリームを生成するモデルに推奨されます。

```csharp
async IAsyncEnumerable<int> GetBigResultsAsync()
{
    await foreach (var result in GetResultsAsync())
    {
        if (result > 20) yield return result;
    }
}
```

`await foreach` を実行できるだけでなく、非同期反復子を作成することもできます。たとえば、`await` と`yield` の両方を行うことができる `IAsyncEnumerable/IAsyncEnumerator` を返す反復子です。 破棄する必要があるオブジェクトの場合は、`Stream` や `Timer` など、さまざまな BCL 型が実装する `IAsyncDisposable` を使用できます。

詳細については、[非同期ストリームのチュートリアル](../../csharp/tutorials/generate-consume-asynchronous-stream.md)を参照してください。

## <a name="ieee-floating-point-improvements"></a>IEEE 浮動小数点の改良

浮動小数点 API は、[IEEE 754-2008 リビジョン](https://en.wikipedia.org/wiki/IEEE_754-2008_revision)に準拠するように更新されます。 これらの変更の目的は、すべての**必要な**操作を公開し、それらの動作が IEEE 仕様に準拠していることを保証することです。浮動小数点の改良の詳細については、「[Floating-Point Parsing and Formatting improvements in .NET Core 3.0 (.NET Core 3.0 の浮動小数点の解析と形式の改良)](https://devblogs.microsoft.com/dotnet/floating-point-parsing-and-formatting-improvements-in-net-core-3-0/)」のブログ記事を参照してください。

次のような解析および書式設定の修正があります。

- 任意の長さの入力を正しく解析して丸める。
- 負のゼロを正しく解析して書式設定する。
- 大文字と小文字を区別しないチェックを実行し、可能な場合には省略可能な先行の `+` を許可することで、`Infinity` と `NaN` を正しく解析する。

新しい <xref:System.Math?displayProperty=nameWithType> API には以下が含まれます。

- <xref:System.Math.BitIncrement(System.Double)> と <xref:System.Math.BitDecrement(System.Double)>\
`nextUp` および `nextDown` の IEEE 演算に相当します。 入力よりも大きいか小さいかを比較する最小の浮動小数点をそれぞれ返します。 たとえば、`Math.BitIncrement(0.0)` は `double.Epsilon` を返します。

- <xref:System.Math.MaxMagnitude(System.Double,System.Double)> と <xref:System.Math.MinMagnitude(System.Double,System.Double)>\
`maxNumMag` および `minNumMag` の IEEE 演算に相当します。2 つの入力の大きさがより大きいまたはより小さい値をそれぞれ返します。 たとえば、`Math.MaxMagnitude(2.0, -3.0)` は `-3.0` を返します。

- <xref:System.Math.ILogB(System.Double)>\
整数値を返す `logB` IEEE 演算に相当します。入力パラメーターの 2 を底とする積分対数を返します。 このメソッドは実質的に `floor(log2(x))` と同じですが、最小限の丸め誤差で実行されます。

- <xref:System.Math.ScaleB(System.Double,System.Int32)>\
整数値を受け取る `scaleB` IEEE 演算に相当します。これは実質的に `x * pow(2, n)` と同じですが、最小限の丸め誤差で実行されます。

- <xref:System.Math.Log2(System.Double)>\
`log2` IEEE 演算に相当します。2 を底とする対数を返します。 丸め誤差を最小限に抑えます。

- <xref:System.Math.FusedMultiplyAdd(System.Double,System.Double,System.Double)>\
`fma` IEEE 演算に相当します。融合型積和演算を実行します。 つまり、単一操作として `(x * y) + z` を実行することで、丸め誤差を最小限に抑えます。 例では、`FusedMultiplyAdd(1e308, 2.0, -1e308)` は `1e308` を返します。 正規の `(1e308 * 2.0) - 1e308` は `double.PositiveInfinity` を返します。

- <xref:System.Math.CopySign(System.Double,System.Double)>\
`copySign` IEEE 演算に相当します。`x` の値を返しますが、`y` の符号と共に返されます。

## <a name="fast-built-in-json-support"></a>高速な組み込み JSON のサポート

.NET ユーザーは、[**Json.NET**](https://www.newtonsoft.com/json) や他のよく使われている JSON ライブラリに大きく依存しています。これは今後も推奨されます。 **Json.NET** では .NET の文字列が基本のデータ型 (内部的には UTF-16) として使用されます。

新しい組み込みの JSON サポートは、高パフォーマンス、低割り当てで、`Span<byte>` に基づいています。 3 つの新しい JSON 関連の主な型が、.NET Core 3.0 の <xref:System.Text.Json?displayProperty=nameWithType> 名前空間に追加されました。 これらの型は、単純な従来の CLR オブジェクト (POCO) のシリアル化と逆シリアル化を "*まだ*" サポートしていません。

### <a name="utf8jsonreader"></a>Utf8JsonReader

<xref:System.Text.Json.Utf8JsonReader?displayProperty=nameWithType> は、UTF-8 でエンコードされた JSON テキスト用の高パフォーマンス、低割り当て、転送のみのリーダーです。`ReadOnlySpan<byte>` から読み取られます。 `Utf8JsonReader` は基本的で低レベルの型であり、カスタム パーサーとデシリアライザーを構築するために使用できます。 新しい `Utf8JsonReader` を使用して JSON ペイロードを読み取る処理は、**Json.NET** のリーダーを使用する場合より 2 倍高速です。 JSON トークンを (UTF-16) 文字列として実現する必要が出てくるまでは割り当てられません。

Visual Studio Code で作成された [**launch.json**](https://github.com/dotnet/samples/blob/master/snippets/core/whats-new/whats-new-in-30/cs/launch.json) ファイルを読み取る例を次に示します。

[!CODE-csharp[Utf8JsonReader](~/samples/snippets/core/whats-new/whats-new-in-30/cs/program.cs#PrintJson)]

[!CODE-csharp[Utf8JsonReader](~/samples/snippets/core/whats-new/whats-new-in-30/cs/program.cs#PrintJsonCall)]

### <a name="utf8jsonwriter"></a>Utf8JsonWriter

<xref:System.Text.Json.Utf8JsonWriter?displayProperty=nameWithType> は、`String`、`Int32`、`DateTime` のような一般的な.NET 型から UTF-8 でエンコードされた JSON テキストを書き込むための、ハイパフォーマンス、非キャッシュ、前方参照専用の方法を提供します。 リーダーと同様に、ライターは基本的で低レベルの型であり、カスタム シリアライザーを構築するために使用できます。 新しい `Utf8JsonWriter` を使用して JSON ペイロードを書き込むと、**Json.NET** からライターを使用するよりも 30 - 80% 高速になり、割り当てが行われません。

### <a name="jsondocument"></a>JsonDocument

<xref:System.Text.Json.JsonDocument?displayProperty=nameWithType> は、`Utf8JsonReader` に基づいています。 `JsonDocument` は、JSON データを解析し、ランダム アクセスと列挙型をサポートするためにクエリできる読み取り専用ドキュメント オブジェクト モデル (DOM) をビルドする機能を提供します。 データを作成する JSON 要素には、`RootElement` というプロパティとして `JsonDocument` によって公開される <xref:System.Text.Json.JsonElement> 型を使用してアクセスできます。 `JsonElement` には、JSON 配列とオブジェクト列挙子とともに、JSON テキストを一般的な .NET 型に変換する API が含まれています。 一般的な JSON ペイロードを解析し、`JsonDocument` を使用してそのメンバーすべてにアクセスすると、適度にサイズ指定された (つまり 1 MB 未満) データに対する割り当てがほとんどない **Json.NET** よりも 2 - 3 倍高速になります。

出発点として使用できる `JsonDocument` および `JsonElement` の使用例を次に示します。

[!CODE-csharp[JsonDocument](~/samples/snippets/core/whats-new/whats-new-in-30/cs/program.cs#ReadJson)]

Visual Studio Code で作成された [**launch.json**](https://github.com/dotnet/samples/blob/master/snippets/core/whats-new/whats-new-in-30/cs/launch.json) ファイルを読み取る C# 8.0 の例を次に示します。

[!CODE-csharp[JsonDocument](~/samples/snippets/core/whats-new/whats-new-in-30/cs/program.cs#ReadJsonCall)]

### <a name="jsonserializer"></a>JsonSerializer

<xref:System.Text.Json.JsonSerializer?displayProperty=nameWithType> は <xref:System.Text.Json.Utf8JsonReader> と <xref:System.Text.Json.Utf8JsonWriter> に基づいて構築されており、JSON ドキュメントやフラグメントを操作する際に高速で低メモリのシリアル化オプションを提供します。

オブジェクトを JSON にシリアル化する例を次に示します。

[!CODE-csharp[JsonSerializer](~/samples/snippets/core/whats-new/whats-new-in-30/cs/JSON.cs#JsonSerialize)]

JSON 文字列をオブジェクトに逆シリアル化する例を次に示します。 前の例で生成された JSON 文字列を使用できます。

[!CODE-csharp[JsonDeserializer](~/samples/snippets/core/whats-new/whats-new-in-30/cs/JSON.cs#JsonDeserialize)]

## <a name="interop-improvements"></a>相互運用性の機能強化

.NET Core 3.0 では、ネイティブ API の相互運用性が強化されました。

### <a name="type-nativelibrary"></a>型:NativeLibrary

<xref:System.Runtime.InteropServices.NativeLibrary?displayProperty=nameWithType> には、(.NET Core P/Invoke と同じ読み込みロジックを使用して) ネイティブ ライブラリを読み込み、`getSymbol` などの関連するヘルパー関数を指定するためのカプセル化機能があります。 コード例については、[DLLMap のデモ](https://github.com/dotnet/samples/tree/master/core/extensions/DllMapDemo)を参照してください。

### <a name="windows-native-interop"></a>Windows のネイティブ相互運用機能

Windows では、フラット C API、COM、および WinRT の形式で、質の高いネイティブ API を提供しています。 .NET Core は **P/Invoke** をサポートしますが、.NET Core 3.0 では **COM API の CoCreate** と **WinRT API のアクティブ化**を行う機能が追加されました。 コード例については、[Excel のデモ](https://github.com/dotnet/samples/tree/master/core/extensions/ExcelDemo)を参照してください。

## <a name="http2-support"></a>HTTP/2 のサポート

<xref:System.Net.Http.HttpClient?displayProperty=nameWithType> 型は HTTP/2 プロトコルをサポートしています。 HTTP/2 が有効な場合、HTTP プロトコルのバージョンは TLS/ALPN を介してネゴシエートされ、HTTP/2 はサーバーがそれを使用することを選択した場合に使用されます。

既定のプロトコルは HTTP/1.1 のままですが、2 つの方法で HTTP/2 を有効にすることができます。 1 つ目として、HTTP/2 を使うように HTTP 要求メッセージを設定することができます。

[!CODE-csharp[Http2Request](~/samples/snippets/core/whats-new/whats-new-in-30/cs/http.cs#Request)]

2 つ目として、既定で HTTP/2 を使うように <xref:System.Net.Http.HttpClient> を変更することができます。

[!CODE-csharp[Http2Client](~/samples/snippets/core/whats-new/whats-new-in-30/cs/http.cs#Client)]

多くの場合、アプリケーションを開発しているときは、暗号化されていない接続を使います。 ターゲット エンドポイントで HTTP/2 が使われることがわかっている場合は、HTTP/2 用の暗号化されていない接続を有効にできます。 有効にするには、`DOTNET_SYSTEM_NET_HTTP_SOCKETSHTTPHANDLER_HTTP2UNENCRYPTEDSUPPORT` 環境変数を `1` に設定するか、またはアプリのコンテキストで有効にします。

[!CODE-csharp[Http2Context](~/samples/snippets/core/whats-new/whats-new-in-30/cs/http.cs#AppContext)]

## <a name="tls-13--openssl-111-on-linux"></a>Linux 上の TLS 1.3 と OpenSSL 1.1.1

.NET Core では、特定の環境で使用できるようになったときに、[OpenSSL 1.1.1 の TLS 1.3 のサポート](https://www.openssl.org/blog/blog/2018/09/11/release111/)を利用できるようになりました。 TLS 1.3 の場合:

- クライアントとサーバー間に必要なラウンド トリップ回数が減るため、接続時間が改善されます。
- 古い安全ではないさまざまな暗号化アルゴリズムが削除されたので、セキュリティが強化されました。

使用できる場合、.NET Core 3.0 では Linux システム上で **OpenSSL 1.1.1**、**OpenSSL 1.1.0**、または **OpenSSL 1.0.2** が使用されます。 **OpenSSL 1.1.1** が使用できる場合、<xref:System.Net.Security.SslStream?displayProperty=nameWithType> 型と <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> 型の両方が **TLS 1.3** を使用します (クライアントとサーバーの両方が **TLS 1.3** をサポートしている場合)。

>[!IMPORTANT]
>Windows と macOS はまだ **TLS 1.3** をサポートしていません。 サポートされるようになったら、.NET Core 3.0 はこれらのオペレーティング システムで **TLS 1.3** をサポートする予定です。

次の C# 8.0 の例は、<https://www.cloudflare.com> に接続している Ubuntu 18.10 上の .NET Core 3.0 を示しています。

[!CODE-csharp[TLSExample](~/samples/snippets/core/whats-new/whats-new-in-30/cs/TLS.cs#TLS)]

## <a name="cryptography-ciphers"></a>暗号化の暗号

.NET 3.0 では、**AES-GCM** および **AES-CCM** の暗号のサポートが追加され、それぞれ <xref:System.Security.Cryptography.AesGcm?displayProperty=nameWithType> および <xref:System.Security.Cryptography.AesCcm?displayProperty=nameWithType> で実装されています。 これらのアルゴリズムは、いずれも [Authenticated Encryption with Association Data (AEAD) アルゴリズム](https://en.wikipedia.org/wiki/Authenticated_encryption)です。

次のコードは、`AesGcm` 暗号を使用してランダム データの暗号化と復号化を行う例です。

[!CODE-csharp[AesGcm](~/samples/snippets/core/whats-new/whats-new-in-30/cs/Cipher.cs#AesGcm)]

## <a name="cryptographic-key-importexport"></a>暗号化キーのインポート/エクスポート

.NET Core 3.0 は、標準形式からの非対称の公開キーと秘密キーのインポートとエクスポートをサポートしています。 X.509 証明書を使用する必要はありません。

*RSA*、*DSA*、*ECDsa*、*ECDiffieHellman* などのすべてのキー種類は、以下の形式をサポートします。

- **公開キー**
  - X.509 SubjectPublicKeyInfo

- **秘密キー**
  - PKCS#8 PrivateKeyInfo
  - PKCS#8 EncryptedPrivateKeyInfo

RSA キーは以下もサポートしています。

- **公開キー**
  - PKCS#1 RSAPublicKey

- **秘密キー**
  - PKCS#1 RSAPrivateKey

エクスポートメソッドからは、DER でエンコードされたバイナリ データが生成され、インポート メソッドもそのようなデータを期待します。 キーがテキストに適した PEM 形式で格納されている場合、呼び出し元は import メソッドを呼び出す前にコンテンツを base64 でデコードする必要があります。

[!CODE-csharp[RSA](~/samples/snippets/core/whats-new/whats-new-in-30/cs/RSA.cs#Rsa)]

**PKCS#8** ファイルは <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo?displayProperty=nameWithType> を使用して検査できます。また、 **PFX/PKCS#12** ファイルは <xref:System.Security.Cryptography.Pkcs.Pkcs12Info?displayProperty=nameWithType> を使用して検査できます。 **PFX/PKCS#12** ファイルは <xref:System.Security.Cryptography.Pkcs.Pkcs12Builder?displayProperty=nameWithType> を使用して操作できます。

## <a name="serialport-for-linux"></a>Linux 用 SerialPort

.Net Core 3.0 では、Linux 上の <xref:System.IO.Ports.SerialPort?displayProperty=nameWithType> に対する基本サポートを提供しています。

以前の .NET Core では、Windows 上の `SerialPort` の使用のみをサポートしていました。

Linux 上のシリアル ポートの制限付きサポートの詳細については、[GitHub 問題 #33146](https://github.com/dotnet/corefx/issues/33146) を参照してください。

## <a name="docker-and-cgroup-memory-limits"></a>Docker と cgroup のメモリ制限

Linux 上の Docker を使用した .NET Core 3.0 の実行は、cgroup のメモリ制限と適切に連携するようになりました。 `docker run -m` のように、メモリ制限を使用して Docker コンテナーを実行すると、.NET Core の動作が変わります。

- 既定のガベージ コレクター (GC) ヒープ サイズ: 最大 20 MB、またはコンテナーのメモリ制限の 75%。
- 明示的なサイズは、cgroup 制限の絶対数または割合として設定できます。
- GC ヒープあたりの最小予約セグメント サイズは 16 MB です。 このサイズによって、マシン上に作成されるヒープ数が減ります。

## <a name="smaller-garbage-collection-heap-sizes"></a>小さいガベージ コレクションのヒープ サイズ

ガベージ コレクターの既定のヒープ サイズが縮小され、.NET Core のメモリ使用量が減少しました。 この変更は、最新のプロセッサ キャッシュ サイズでは、世代 0 の割り当て予算に合わせたものです。

## <a name="garbage-collection-large-page-support"></a>ガベージ コレクションのラージ ページのサポート

ラージ ページ (Linux ではヒュージ ページとも呼ばれます) は、オペレーティング システムがネイティブ ページ サイズ (多くの場合は 4K) よりも大きいメモリ領域を確立して、このようなラージ ページを要求するアプリケーションのパフォーマンスを向上できる機能です。

Windows 上でラージ ページを割り当てることを選択するオプトイン機能として、**GCLargePages** 設定を使用してガベージ コレクターを構成できるようになりました。

## <a name="gpio-support-for-raspberry-pi"></a>Raspberry Pi の GPIO サポート

GPIO プログラミングに使用できる 2 つのパッケージが NuGet にリリースされました。

- [System.Device.Gpio](https://www.nuget.org/packages/System.Device.Gpio)
- [Iot.Device.Bindings](https://www.nuget.org/packages/Iot.Device.Bindings)

GPIO パッケージには、*GPIO*、*SPI*、*I2C*、および *PWM* デバイス用の API が含まれています。 IoT バインディング パッケージにはデバイス バインディングが含まれています。 詳細については、[デバイス GitHub リポジトリ](https://github.com/dotnet/iot/blob/master/src/devices/)を参照してください。

## <a name="arm64-linux-support"></a>ARM64 Linux のサポート

.NET Core 3.0 では、Linux 用の ARM64 のサポートが追加されています。 現在、ARM64 の主なユース ケースは、IoT シナリオを使用しています。 詳細については、[.NET Core ARM64 の状態](https://github.com/dotnet/announcements/issues/82)に関する記事を参照してください。

[ARM64 上の .NET Core 用の Docker イメージ](https://hub.docker.com/r/microsoft/dotnet/)は、Alpine、Debian、および Ubuntu に使用できます。

> [!NOTE]
> **ARM64** Windows のサポートはまだ使用できません。
