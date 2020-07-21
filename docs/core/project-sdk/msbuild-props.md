---
title: Microsoft.NET.Sdk の MSBuild プロパティ
description: .NET Core SDK によって認識される MSBuild のプロパティと項目のリファレンスです。
ms.date: 02/14/2020
ms.topic: reference
ms.openlocfilehash: cda56b3e23592a341d9fe672fc1f1530adcdab49
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83206107"
---
# <a name="msbuild-reference-for-net-core-sdk-projects"></a>.NET Core SDK プロジェクトの MSBuild リファレンス

このページは、.NET Core プロジェクトの構成に使用できる、MSBuild のプロパティと項目のリファレンスです。

> [!NOTE]
> このページの編集は進行中であり、.NET Core SDK の便利な MSBuild プロパティがすべて記載されている訳ではありません。 一般的な MSBuild プロパティの一覧については、「[MSBuild プロジェクトの共通プロパティ](/visualstudio/msbuild/common-msbuild-project-properties)」を参照してください。

## <a name="framework-properties"></a>フレームワークのプロパティ

- [TargetFramework](#targetframework)
- [TargetFrameworks](#targetframeworks)
- [NetStandardImplicitPackageVersion](#netstandardimplicitpackageversion)

### <a name="targetframework"></a>TargetFramework

`TargetFramework` プロパティには、[ メタパッケージ ](../packages.md#metapackages) を暗黙的に参照するアプリのターゲット フレームワーク バージョンを指定します。 有効なターゲット フレームワーク モニカーの一覧については、「[SDK スタイルのプロジェクトでのターゲット フレームワーク](../../standard/frameworks.md#supported-target-framework-versions)」を参照してください。

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
```

詳細については、「[SDK スタイルのプロジェクトでのターゲット フレームワーク](../../standard/frameworks.md)」を参照してください。

### <a name="targetframeworks"></a>TargetFrameworks

アプリで複数のプラットフォームをターゲットにする場合は、`TargetFrameworks` プロパティを使用します。 有効なターゲット フレームワーク モニカーの一覧については、「[SDK スタイルのプロジェクトでのターゲット フレームワーク](../../standard/frameworks.md#supported-target-framework-versions)」を参照してください。

> [!NOTE]
> `TargetFramework` (単数形) が指定されている場合、このプロパティは無視されます。

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp3.1;net462</TargetFrameworks>
</PropertyGroup>
```

詳細については、「[SDK スタイルのプロジェクトでのターゲット フレームワーク](../../standard/frameworks.md)」を参照してください。

### <a name="netstandardimplicitpackageversion"></a>NetStandardImplicitPackageVersion

> [!NOTE]
> このプロパティは、`netstandard1.x` を使用するプロジェクトにのみ適用されます。 `netstandard2.x` を使用するプロジェクトには適用されません。

[メタパッケージ](../packages.md#metapackages) バージョンよりも低いフレームワーク バージョンを指定する場合は、`NetStandardImplicitPackageVersion` プロパティを使用します。 次の例のプロジェクト ファイルは、`netstandard1.3` をターゲットにしていますが、`NETStandard.Library` の 1.6.0 バージョンを使用しています。

```xml
<PropertyGroup>
  <TargetFramework>netstandard1.3</TargetFramework>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

## <a name="package-properties"></a>パッケージのプロパティ

`PackageId`、`PackageVersion`、`PackageIcon`、`Title`、`Description` などのプロパティを指定し、プロジェクトから作成されたパッケージについて説明できます。 以上のプロパティとその他のプロパティの詳細については、「[pack ターゲット](/nuget/reference/msbuild-targets#pack-target)」を参照してください。

```xml
<PropertyGroup>
  ...
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>John Doe</Authors>
  <Company>Contoso</Company>
</PropertyGroup>
```

## <a name="publish-properties-and-items"></a>プロパティと項目の発行

- [RuntimeIdentifier](#runtimeidentifier)
- [RuntimeIdentifiers](#runtimeidentifiers)
- [TrimmerRootAssembly](#trimmerrootassembly)
- [UseAppHost](#useapphost)

### <a name="runtimeidentifier"></a>RuntimeIdentifier

`RuntimeIdentifier` プロパティを使用すると、プロジェクトに 1 つの[ランタイム識別子 (RID)](../rid-catalog.md) を指定できます。 RID により、自己完結型の展開を発行できます。

```xml
<PropertyGroup>
  <RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
</PropertyGroup>
```

### <a name="runtimeidentifiers"></a>RuntimeIdentifiers

`RuntimeIdentifiers` プロパティには、プロジェクトの[ランタイム識別子 (RID)](../rid-catalog.md) のセミコロン区切りリストを指定できます。 複数のランタイムに発行する必要がある場合は、このプロパティを使用します。 `RuntimeIdentifiers` は、復元時に適切な資産をグラフに確実に含めるために使用されます。

> [!TIP]
> `RuntimeIdentifier` (単数形) を使用すると、必要なランタイムが 1 つだけのとき、ビルドが速くなります。

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="trimmerrootassembly"></a>TrimmerRootAssembly

`TrimmerRootAssembly` 項目ではアセンブリを "[*トリミング*](../deploying/trim-self-contained.md)" から除外できます。 トリミングとは、パッケージ化されたアプリケーションからランタイムの未使用部分を削除するプロセスです。 必要な参照がトリミングによって間違って削除されることもあります。

次の XML では、トリミングから `System.Security` アセンブリが除外されます。

```xml
<ItemGroup>
  <TrimmerRootAssembly Include="System.Security" />
</ItemGroup>
```

### <a name="useapphost"></a>UseAppHost

`UseAppHost` プロパティは、.NET Core SDK の 2.1.400 バージョンで導入されました。 デプロイ用にネイティブ実行可能ファイルを作成するかどうかを制御できます。 自己完結型の配置にはネイティブの実行可能ファイルが必要です。

.NET Core 3.0 以降のバージョンでは、既定でフレームワークに依存する実行可能ファイルが作成されます。 実行可能ファイルの生成を無効にするには、`UseAppHost` プロパティを `false` に設定します。

```xml
<PropertyGroup>
  <UseAppHost>false</UseAppHost>
</PropertyGroup>
```

配置の詳細については、[.NET Core アプリケーションの配置](../deploying/index.md)に関するページを参照してください。

## <a name="compile-properties"></a>コンパイルのプロパティ

- [EmbeddedResourceUseDependentUponConvention](#embeddedresourceusedependentuponconvention)
- [LangVersion](#langversion)

### <a name="embeddedresourceusedependentuponconvention"></a>EmbeddedResourceUseDependentUponConvention

`EmbeddedResourceUseDependentUponConvention` プロパティは、リソース マニフェスト ファイル名が、リソース ファイルと併置されているソース ファイルの型情報から生成されるかどうかを定義します。 たとえば、*Form1.vb* が *Form1.cs* と同じフォルダーにあり、`EmbeddedResourceUseDependentUponConvention` が `true` に設定されている場合、生成された *.resources* ファイルは *Form1.cs* で定義されている最初の型から名前を受け取ります。 たとえば、`MyNamespace.Form1` が *Form1.cs* で定義されている最初の型である場合、生成されたファイル名は *MyNamespace.Form1.resources* になります。

> [!NOTE]
> `LogicalName`、`ManifestResourceName`、または `DependentUpon` メタデータが `EmbeddedResource` 項目に対して指定されている場合、そのリソース ファイルに対して生成されたマニフェスト ファイル名は、代わりにそのメタデータがベースになります。

既定では、新しい .NET Core プロジェクトでは、このプロパティは `true` に設定されます。 `false` に設定され、かつプロジェクト ファイルの `EmbeddedResource` 項目に `LogicalName`、`ManifestResourceName`、`DependentUpon` のメタデータがどれも指定されていない場合、リソース マニフェストのファイル名は、プロジェクトのルート名前空間と、 *.resx* ファイルへの相対ファイル パスがベースになります。 詳細については、「[リソース マニフェスト ファイルの名前付けの方法](../resources/manifest-file-names.md)」を参照してください。

```xml
<PropertyGroup>
  <EmbeddedResourceUseDependentUponConvention>true</EmbeddedResourceUseDependentUponConvention>
</PropertyGroup>
```

### <a name="langversion"></a>LangVersion

`LangVersion` プロパティを使用すると、特定のプログラミング言語バージョンを指定できます。 たとえば、C# プレビュー機能にアクセスする場合は、`LangVersion` を `preview` に設定します。

```xml
<PropertyGroup>
  <LangVersion>preview</LangVersion>
</PropertyGroup>
```

詳細については、「[C# 言語のバージョン管理](../../csharp/language-reference/configure-language-version.md#override-a-default)」を参照してください。

## <a name="run-time-configuration-properties"></a>ランタイム構成プロパティ

アプリのプロジェクト ファイルに MSBuild プロパティを指定することで一部のランタイム動作を構成できます。 ランタイム動作のその他の構成方法については、「[.NET Core ランタイム構成設定](../run-time-config/index.md)」を参照してください。

- [ConcurrentGarbageCollection](#concurrentgarbagecollection)
- [InvariantGlobalization](#invariantglobalization)
- [RetainVMGarbageCollection](#retainvmgarbagecollection)
- [ServerGarbageCollection](#servergarbagecollection)
- [ThreadPoolMaxThreads](#threadpoolmaxthreads)
- [ThreadPoolMinThreads](#threadpoolminthreads)
- [TieredCompilation](#tieredcompilation)
- [TieredCompilationQuickJit](#tieredcompilationquickjit)
- [TieredCompilationQuickJitForLoops](#tieredcompilationquickjitforloops)

### <a name="concurrentgarbagecollection"></a>ConcurrentGarbageCollection

`ConcurrentGarbageCollection` プロパティでは、[バックグラウンド (同時実行) ガベージ コレクション](../../standard/garbage-collection/background-gc.md)の有効または無効が設定されます。 この値を `false` に設定すると、バックグラウンド ガベージ コレクションが無効になります。 詳細については、「[System.GC.Concurrent/COMPlus_gcConcurrent](../run-time-config/garbage-collector.md#systemgcconcurrentcomplus_gcconcurrent)」を参照してください。

```xml
<PropertyGroup>
  <ConcurrentGarbageCollection>false</ConcurrentGarbageCollection>
</PropertyGroup>
```

### <a name="invariantglobalization"></a>InvariantGlobalization

`InvariantGlobalization` プロパティでは、アプリを *globalization-invariant* モードで実行するかどうかを設定します。このモードでは、カルチャ固有のデータにアクセスできません。 この値を `true` に設定すると、globalization-invariant モードで実行されます。 詳細については、「[インバリアント モード](../run-time-config/globalization.md#invariant-mode)」を参照してください。

```xml
<PropertyGroup>
  <InvariantGlobalization>true</InvariantGlobalization>
</PropertyGroup>
```

### <a name="retainvmgarbagecollection"></a>RetainVMGarbageCollection

`RetainVMGarbageCollection` プロパティでは、将来利用する目的で削除済みメモリ セグメントを待機一覧に載せるように、あるいは削除済みメモリ セグメントを解放するようにガベージ コレクターを設定します。 この値を `true` に設定すると、セグメントを待機一覧に載せるよう、ガベージ コレクターが命令されます。 詳細については、「[System.GC.RetainVM/COMPlus_GCRetainVM](../run-time-config/garbage-collector.md#systemgcretainvmcomplus_gcretainvm)」を参照してください。

```xml
<PropertyGroup>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
</PropertyGroup>
```

### <a name="servergarbagecollection"></a>ServerGarbageCollection

`ServerGarbageCollection` プロパティでは、アプリケーションで使用するガベージ コレクションとして[ワークステーション ガベージ コレクションまたはサーバー ガベージ コレクション](../../standard/garbage-collection/workstation-server-gc.md)を設定します。 この値を `true` に設定すると、サーバー ガベージ コレクションが使用されます。 詳細については、「[System.GC.Server/COMPlus_gcServer](../run-time-config/garbage-collector.md#systemgcservercomplus_gcserver)」を参照してください。

```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

### <a name="threadpoolmaxthreads"></a>ThreadPoolMaxThreads

`ThreadPoolMaxThreads` プロパティでは、ワーカー スレッド プールの最大スレッド数を設定します。 詳細については、「[最大スレッド数](../run-time-config/threading.md#maximum-threads)」を参照してください。

```xml
<PropertyGroup>
  <ThreadPoolMaxThreads>20</ThreadPoolMaxThreads>
</PropertyGroup>
```

### <a name="threadpoolminthreads"></a>ThreadPoolMinThreads

`ThreadPoolMinThreads` プロパティでは、ワーカー スレッド プールの最小スレッド数を設定します。 詳細については、「[最小スレッド数](../run-time-config/threading.md#minimum-threads)」を参照してください。

```xml
<PropertyGroup>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
</PropertyGroup>
```

### <a name="tieredcompilation"></a>TieredCompilation

`TieredCompilation` プロパティでは、Just-In-Time (JIT) コンパイラで[階層型コンパイル](../whats-new/dotnet-core-3-0.md#tiered-compilation)を使用するかどうかを設定します。 この値を `false` に設定すると、階層型コンパイルが無効になります。 詳細については、「[階層型コンパイル](../run-time-config/compilation.md#tiered-compilation)」を参照してください。

```xml
<PropertyGroup>
  <TieredCompilation>false</TieredCompilation>
</PropertyGroup>
```

### <a name="tieredcompilationquickjit"></a>TieredCompilationQuickJit

`TieredCompilationQuickJit` プロパティでは、JIT コンパイラでクイック JIT を使用するかどうかを設定します。 この値を `false` に設定すると、クイック JIT が無効になります。 詳細については、「[クイック JIT](../run-time-config/compilation.md#quick-jit)」を参照してください。

```xml
<PropertyGroup>
  <TieredCompilationQuickJit>false</TieredCompilationQuickJit>
</PropertyGroup>
```

### <a name="tieredcompilationquickjitforloops"></a>TieredCompilationQuickJitForLoops

`TieredCompilationQuickJitForLoops` プロパティでは、ループを含むメソッドに対して JIT コンパイラでクリック JIT を使用するかどうかを設定します。 この値を `true` に設定すると、ループが含まれるメソッドでクイック JIT が有効になります。 詳細については、「[ループに対するクイック JIT](../run-time-config/compilation.md#quick-jit-for-loops)」を参照してください。

```xml
<PropertyGroup>
  <TieredCompilationQuickJitForLoops>true</TieredCompilationQuickJitForLoops>
</PropertyGroup>
```

## <a name="reference-properties-and-items"></a>プロパティと項目の参照

- [AssetTargetFallback](#assettargetfallback)
- [PackageReference](#packagereference)
- [ProjectReference](#projectreference)
- [参照](#reference)
- [Restore プロパティ](#restore-properties)

### <a name="assettargetfallback"></a>AssetTargetFallback

`AssetTargetFallback` プロパティを使用すると、プロジェクト参照と NuGet パッケージに対して、互換性のある追加のフレームワーク バージョンを指定できます。 たとえば、`PackageReference` を使用してパッケージの依存関係を指定し、そのパッケージにプロジェクトの `TargetFramework` と互換性のある資産が含まれない場合は、`AssetTargetFallback` プロパティが機能します。 参照されたパッケージの互換性は、`AssetTargetFallback` で指定された各ターゲット フレームワークを使用して再確認されます。

`AssetTargetFallback` プロパティを 1 つ以上の[ターゲット フレームワーク バージョン](../../standard/frameworks.md#supported-target-framework-versions)に設定できます。

```xml
<PropertyGroup>
  <AssetTargetFallback>net461</AssetTargetFallback>
</PropertyGroup>
```

### <a name="packagereference"></a>PackageReference

`PackageReference` 項目では、NuGet パッケージへの参照が定義されます。 たとえば、[メタパッケージ](../packages.md#metapackages)ではなく 1 つのパッケージを参照する場合があります。

`Include` 属性は、パッケージ ID を指定します。 `Version` 属性では、バージョンまたはバージョン範囲を指定します。 最小バージョン、最大バージョン、範囲、厳密一致を指定する方法については、「[バージョン範囲](/nuget/concepts/package-versioning#version-ranges)」を参照してください。 また、メタデータ `IncludeAssets`、`ExcludeAssets`、`PrivateAssets` をプロジェクト参照に追加できます。

次の例のプロジェクト ファイル スニペットでは、[System.Runtime](https://www.nuget.org/packages/System.Runtime/) パッケージを参照しています。

```xml
<ItemGroup>
  <PackageReference Include="System.Runtime" Version="4.3.0" />
</ItemGroup>
```

詳細については、[プロジェクト ファイルのパッケージ参照](/nuget/consume-packages/package-references-in-project-files)に関するページを参照してください。

### <a name="projectreference"></a>ProjectReference

`ProjectReference` 項目では、別のプロジェクトへの参照を定義します。 参照されたプロジェクトは NuGet パッケージ依存関係として追加されます。つまり、`PackageReference` と同じように処理されます。

`Include` 属性は、プロジェクトのパスを指定します。 また、メタデータ `IncludeAssets`、`ExcludeAssets`、`PrivateAssets` をプロジェクト参照に追加できます。

次の例のプロジェクト ファイル スニペットでは、`Project2` という名前のプロジェクトが参照されます。

```xml
<ItemGroup>
  <ProjectReference Include="..\Project2.csproj" />
</ItemGroup>
```

### <a name="reference"></a>関連項目

`Reference` 項目では、アセンブリ ファイルへの参照を定義します。

`Include` 属性によってファイルの名前が指定され、`HintPath` メタデータによってアセンブリへのパスが指定されます。

```xml
<ItemGroup>
  <Reference Include="MyAssembly">
    <HintPath>..\..\Assemblies\MyAssembly.dll</HintPath>
  </Reference>
</ItemGroup>
```

### <a name="restore-properties"></a>restore のプロパティ

参照されたパッケージを復元すると、その直接的な依存関係と間接的な依存関係がすべてインストールされます。 `RestorePackagesPath` や `RestoreIgnoreFailedSources` など、プロパティを指定することでパッケージ復元をカスタマイズできます。 以上のプロパティとその他のプロパティの詳細については、「[restore ターゲット](/nuget/reference/msbuild-targets#restore-target)」を参照してください。

```xml
<PropertyGroup>
  <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

## <a name="see-also"></a>関連項目

- [MSBuild スキーマ リファレンス](/visualstudio/msbuild/msbuild-project-file-schema-reference)
- [MSBuild の共通プロパティ](/visualstudio/msbuild/common-msbuild-project-properties)
- [NuGet pack の MSBuild プロパティ](/nuget/reference/msbuild-targets#pack-target)
- [NuGet restore の MSBuild プロパティ](/nuget/reference/msbuild-targets#restore-properties)
- [ビルドのカスタマイズ](/visualstudio/msbuild/customize-your-build)
