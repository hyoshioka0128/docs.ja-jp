---
ms.openlocfilehash: f24a29a00a1bff34a452c43716d76bf72ef277b5
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83206222"
---
### <a name="resource-manifest-file-name-change"></a>リソース マニフェストのファイル名の変更

.NET Core 3.0 以降では、既定の場合、MSBuild によってリソース ファイルに対して異なるマニフェスト ファイル名が生成されます。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="change-description"></a>変更の説明

.NET Core 3.0 より前では、プロジェクト ファイルの `EmbeddedResource` 項目に `LogicalName`、`ManifestResourceName`、または `DependentUpon` メタデータが指定されなかった場合、MSBuild ではパターン `<RootNamespace>.<ResourceFilePathFromProjectRoot>.resources` でマニフェスト ファイル名が生成されていました。 `RootNamespace` がプロジェクト ファイルで定義されていない場合は、既定でそのプロジェクトの名前になります。 たとえば、ルート プロジェクト ディレクトリ内の *Form1* という名前のリソース ファイルに対して生成されたマニフェスト名は、*MyProject.Form1.resources* でした。

.NET Core 3.0 以降では、あるリソース ファイルが同じ名前のソース ファイルと併置されている場合 (たとえば、*Form1.resx* と *Form1.cs*)、MSBuild ではそのソース ファイルの型情報が使用されてパターン `<Namespace>.<ClassName>.resources` でマニフェスト ファイル名が生成されます。 名前空間とクラス名は、併置されたソース ファイルの最初の型から抽出されます。 たとえば、*Form1.cs* という名前のソース ファイルと併置されている *Form1* という名前のリソース ファイルに対して生成されたマニフェスト名は、*MyNamespace.Form1.resources* になります。 重要な注意点として、.NET Core の以前のバージョンとはファイル名の最初の部分が異なります (*MyProject* ではなく *MyNamespace*)。

> [!NOTE]
> プロジェクト ファイルの `EmbeddedResource` 項目で `LogicalName`、`ManifestResourceName`、または `DependentUpon` メタデータが指定されている場合、この変更はそのリソース ファイルには影響しません。

この破壊的変更は、.NET Core プロジェクトへの `EmbeddedResourceUseDependentUponConvention` プロパティの追加によって導入されました。 既定では、リソース ファイルは .NET Core プロジェクト ファイルに明示的にリストされていないため、生成された *.resources* ファイルに名前を付ける方法を指定するための `DependentUpon` メタデータはありません。 `EmbeddedResourceUseDependentUponConvention` が `true` に設定されている場合 (既定)、MSBuild では併置されたソース ファイルが検索され、そのファイルから名前空間とクラス名が抽出されます。 `EmbeddedResourceUseDependentUponConvention` を `false` に設定すると、MSBuild では `RootNamespace` と相対ファイル パスを組み合わせた前の動作に従ってマニフェスト名が生成されます。

#### <a name="recommended-action"></a>推奨アクション

ほとんどの場合、開発者側でアクションを取る必要はなく、アプリは引き続き動作するはずです。 ただし、この変更によってアプリに影響が出ている場合は、次のいずれかを実行してください。

- 新しいマニフェスト名を要求するようにコードを変更する。

- プロジェクト ファイルで `EmbeddedResourceUseDependentUponConvention` を `false` に設定して、新しい名前付け規則を無効にする。

  ```xml
  <PropertyGroup>
    <EmbeddedResourceUseDependentUponConvention>false</EmbeddedResourceUseDependentUponConvention>
  </PropertyGroup>
  ```

#### <a name="category"></a>カテゴリ

MSBuild

#### <a name="affected-apis"></a>影響を受ける API

N/A
