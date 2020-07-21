---
title: 自己完結型アプリケーションのトリミング
description: 自己完結型アプリケーションをトリミングしてサイズを縮小する方法について説明します。 .NET Core は、自己完結型で公開されているアプリケーションでランタイムをバンドルし、通常は必要以上のランタイムを含んでいます。
author: jamshedd
ms.author: jamshedd
ms.date: 04/03/2020
ms.openlocfilehash: bb8ac88c5e16b7fd20a7670e4ad76dbe4b44da1b
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81242916"
---
# <a name="trim-self-contained-deployments-and-executables"></a>自己完結型の展開と実行可能ファイルのトリミング

自己完結型アプリケーションを公開する場合、.NET Core ランタイムにはアプリケーションもバンドルされます。 このバンドルにより、パッケージ アプリケーションに大量のコンテンツが追加されます。 アプリケーションの展開では、多くの場合、サイズが重要な要素になります。 通常は、パッケージ アプリケーションのサイズをなるべく小さく保つことが、アプリケーション開発者の目標となります。

アプリケーションの複雑さによっては、アプリケーションの実行にランタイムのサブセットだけが必要となります。 このようなランタイムの未使用部分は不要であり、パッケージ化されたアプリケーションから削除することができます。

トリミング機能は、アプリケーション バイナリを調べて、必要なランタイム アセンブリのグラフを検出し、構築することで機能します。 参照されていないその他のランタイム アセンブリは除外されます。

> [!NOTE]
> トリミングは .NET Core 3.1 の実験的な機能であり、自己完結型で公開されるアプリケーションで_のみ_使用できます。

## <a name="prevent-assemblies-from-being-trimmed"></a>アセンブリがトリミングされないようにする

トリミング機能が参照の検出に失敗するシナリオがあります。 たとえば、アプリケーションまたはアプリケーションによって参照されるライブラリから、ランタイム アセンブリに対してリフレクションが使用されている場合、アセンブリは直接参照されません。 このような間接参照はトリミングに認識されず、ライブラリは発行フォルダーから除外されます。

コードからリフレクションを介して間接的にアセンブリを参照している場合は、`<TrimmerRootAssembly>` 設定を使用してアセンブリがトリミングされないようにすることができます。 次の例は、`System.Security` アセンブリという名前のアセンブリがトリミングされないようにする方法を示しています。

```xml
<ItemGroup>
    <TrimmerRootAssembly Include="System.Security" />
</ItemGroup>
```

## <a name="trim-your-app---cli"></a>アプリをトリミングする - CLI

[dotnet publish](../tools/dotnet-publish.md) コマンドを使用してアプリケーションをトリミングします。 アプリを発行するときは、次の 3 つの設定を設定します。

- 自己完結型として発行する: `--self-contained true`
- 単一ファイルの発行を無効にする: `-p:PublishSingleFile=false`
- トリミングを有効にする: `p:PublishTrimmed=true`

次の例では、Windows 10 用のアプリを自己完結型として発行し、出力をトリミングします。

```dotnetcli
dotnet publish -c Release -r win10-x64 --self-contained true -p:PublishSingleFile=false -p:PublishTrimmed=true
```

詳細については、「[.NET Core CLI を使用して .NET Core アプリを発行する](deploy-with-cli.md)」を参照してください。

## <a name="trim-your-app---visual-studio"></a>アプリをトリミングする - Visual Studio

Visual Studio を使用すると、アプリケーションの発行方法を制御する再利用可能な発行プロファイルを作成できます。

01. **[ソリューション エクスプローラー]** ペインで、発行するプロジェクトを右クリックします。 **[発行]** を選択します。

    :::image type="content" source="media/trim-self-contained/visual-studio-solution-explorer.png" alt-text="右クリック メニューの [発行] オプションが強調表示されたソリューション エクスプローラー。":::

    発行プロファイルがまだない場合は、指示に従って作成し、ターゲットの種類として **[フォルダー]** を選択します。

01. **[編集]** を選択します。

    :::image type="content" source="media/trim-self-contained/visual-studio-publish-edit-settings.png" alt-text="Visual Studio の発行プロファイルと [編集] ボタン":::

01. **[プロファイル設定]** ダイアログで、次のオプションを設定します。

    - **[配置モード]** を **[自己完結]** に設定します。
    - **[ターゲット ランタイム]** を発行先のプラットフォームに設定します。
    - **[未使用のアセンブリをトリミングする (プレビュー)]** を選択します。

    **[保存]** を選択して設定を保存し、 **[発行]** ダイアログに戻ります。

    :::image type="content" source="media/trim-self-contained/visual-studio-publish-properties.png" alt-text="[配置モード]、[ターゲット ランタイム]、[未使用のアセンブリをトリミングする] オプションが強調表示されている [プロファイル設定] ダイアログ。":::

01. **[発行]** を選択してトリミングされたアプリを発行します。

詳細については、[Visual Studio を使用した .NET Core アプリの発行](deploy-with-vs.md)に関するページを参照してください。

## <a name="trim-your-app---visual-studio-for-mac"></a>アプリをトリミングする - Visual Studio for Mac

Visual Studio for Mac には、発行時にアプリをトリミングするオプションがありません。 「[アプリをトリミングする - CLI](#trim-your-app---cli)」セクションの手順に従って手動で発行する必要があります。 詳細については、「[.NET Core CLI を使用して .NET Core アプリを発行する](deploy-with-cli.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [.NET Core アプリケーションの配置](index.md)。
- [.NET Core CLI を使用して .NET Core アプリを発行する](deploy-with-cli.md)。
- [Visual Studio を使用して .NET Core アプリを発行する](deploy-with-vs.md)。
- [dotnet publish コマンド](../tools/dotnet-publish.md)。
