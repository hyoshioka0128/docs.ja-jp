---
title: ソース リンクと .NET ライブラリ
description: ソース リンクを使用して .NET ライブラリのデバッグ機能を改善するためのベスト プラクティス推奨事項。
ms.date: 01/15/2019
ms.openlocfilehash: 5dee2a6b1f77daa641351e02c1dd3e0a38f66550
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84201984"
---
# <a name="source-link"></a>ソース リンク

ソース リンクは NuGet からの .NET アセンブリのソース コードを開発者がデバッグすることを可能にするテクノロジです。 ソース リンクは NuGet パッケージの作成時に実行され、ソース コントロール メタデータをアセンブリとパッケージの内部に埋め込みます。 パッケージをダウンロードし、Visual Studio でソース リンクを有効にした開発者は、そのソース コードにステップ インできます。 ソース リンクからは、効率的なデバッグを可能にするソース コントロール メタデータが提供されます。

## <a name="source-link-demo"></a>ソース リンクのデモ

<!--markdownlint-disable MD034 -->
> [!VIDEO https://www.youtube.com/embed/gyRGhCQPkB4?start=61]

## <a name="using-source-link"></a>ソース リンクを使用する

ソース リンクの使用方法は、[dotnet/sourcelink](https://github.com/dotnet/sourcelink/blob/master/README.md) GitHub リポジトリにあります。

[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)を使用すれば、ソース リンク メタデータがパッケージに正常に埋め込まれたことを確認できます。 `Repository` メタデータがコミット ID と共に存在すること、各ターゲットの .dll と共に .pdb ファイルが見つかることを確認します。

![NuGet パッケージ エクスプローラーのソース リンク](./media/sourcelink/nuget-package-explorer-sourcelink.png "NuGet パッケージ エクスプローラーのソース リンク")

✔️ 検討 ソース リンクを使用して、お使いのアセンブリと NuGet パッケージにソース管理のメタデータを追加する。

> [!TIP]
> デバッガー属性を型に追加することで開発者のデバッグ機能をさらに強化できます。
>
> * <xref:System.Diagnostics.DebuggerDisplayAttribute> では、デバッガーの変数ウィンドウでクラスやフィールドを表示する方法をカスタマイズできます。
> * <xref:System.Diagnostics.DebuggerStepThroughAttribute> では、デバッガーに対してコードのステップ インではなくステップ実行が指示されます。
> * <xref:System.Diagnostics.DebuggerBrowsableAttribute> では、デバッガー変数ウィンドウにメンバーを表示するかどうかが制御されます。

✔️ 検討 シンボル ファイルを発行する (`*.pdb`)。

> デバッグのエクスペリエンスを最善にするには、ライブラリ上でシンボル ファイルを発行してソース リンクを使用する必要があります。 シンボル ファイルとシンボル パッケージの詳細については、「[シンボル パッケージ](./nuget.md#symbol-packages)」を参照してください。

✔️ 検討 決定論的ビルドを有効にする

> 決定論的ビルドでは、結果として得られるバイナリが指定されたソースから構築され、追跡可能性を提供することの検証を可能にします。 決定論的ビルドとそれを有効にするための手順の詳細については、[決定論的ビルド](https://github.com/clairernovotny/DeterministicBuilds)に関するページを参照してください。

>[!div class="step-by-step"]
>[前へ](dependencies.md)
>[次へ](publish-nuget-package.md)
