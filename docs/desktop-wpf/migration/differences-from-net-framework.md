---
title: .NET Framework と .NET Core の相違点
description: Windows Presentation Foundation (WPF) の .NET Framework の実装と .NET Core の WPF との相違点について説明します。 アプリを移行するときは、次の非互換性について考慮する必要があります。
author: adegeo
ms.date: 09/21/2019
ms.author: adegeo
ms.openlocfilehash: 3bedc30046c36d4c5430feedf5854276ebaef8aa
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325694"
---
# <a name="differences-in-wpf"></a>WPF の相違点

この記事では、.NET Core と .NET Framework での Windows Presentation Foundation (WPF) の違いについて説明します。 .NET Core の WPF は、.NET Framework ソース コードの元の WPF からフォークされた [オープンソース フレームワーク](https://github.com/dotnet/wpf)です。

.NET Framework の機能のうち、.NET Core ではサポートされないものがいくつかあります。 サポートされないテクノロジの詳細については、「[.NET Core で使用できない .NET Framework テクノロジ](../../core/porting/net-framework-tech-unavailable.md)」を参照してください。

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

## <a name="sdk-style-projects"></a>SDK スタイルのプロジェクト

.NET Core では、SDK スタイルのプロジェクト ファイルが使用されます。 これらのプロジェクト ファイルは、Visual Studio によって管理される従来の .NET Framework プロジェクト ファイルとは異なります。 .NET Framework の WPF アプリを .NET Core に移行するには、プロジェクトを変換する必要があります。 詳細については、「[.NET Core 3.0 への WPF アプリの移行](convert-project-from-net-framework.md)」を参照してください。

## <a name="nuget-package-references"></a>NuGet パッケージのリファレンス

.NET Framework アプリで *packages.config* ファイルに NuGet の依存関係が一覧表示されている場合は、[`<PackageReference>`](/nuget/consume-packages/package-references-in-project-files) 形式に移行します。

1. Visual Studio で、 **[ソリューション エクスプローラー]** ペインを開きます。
1. WPF プロジェクトで、右クリックで **[packages.config]**  >  **[packages.config を PackageReference に移行する]** と進みます。

![PackageReference へのアップグレード](media/differences-from-net-framework/package-reference-migration.png)

計算された最上位の NuGet 依存関係を表示し、他のどの NuGet パッケージを最上位に昇格する必要があるかを尋ねるダイアログが表示されます。 **[OK]** を選択すると、*packages.config* ファイルがプロジェクトから削除され、`<PackageReference>` 要素がプロジェクト ファイルに追加されます。

プロジェクトで `<PackageReference>` を使用する場合、パッケージは *Packages* フォルダーにローカルに保存されず、グローバルに格納されます。 プロジェクト ファイルを開き、*Packages* フォルダーを参照していた `<Analyzer>` 要素をすべて削除します。 これらのアナライザーは、NuGet パッケージの参照に自動的に含まれます。

## <a name="code-access-security"></a>コード アクセス セキュリティ

コード アクセス セキュリティ (CAS) は、.Net Core でも .NET Core の WPF でもサポートされません。 CAS 関連のすべての機能は、完全な信頼の想定のもとで扱われます。 .NET Core の WPF では、CAS 関連のコードは削除されます。 これらの型のパブリック API サーフェイスは、これらの型への呼び出しが成功するように引き続き存在しています。

パブリックに定義された CAS 関連の型は、WPF アセンブリから Core .NET ライブラリ アセンブリに移動されました。 WPF アセンブリでは、型転送が、移動された型の新しい場所に設定されています。

| ソース アセンブリ | ターゲット アセンブリ | 種類                |
| --------------- | --------------- | ------------------- |
| *WindowsBase.dll* | *System.Security.Permissions.dll* | <xref:System.Security.Permissions.MediaPermission> <br /> <xref:System.Security.Permissions.MediaPermissionAttribute> <br /> <xref:System.Security.Permissions.MediaPermissionAudio> <br /> <xref:System.Security.Permissions.MediaPermissionImage> <br /> <xref:System.Security.Permissions.MediaPermissionVideo> <br /> <xref:System.Security.Permissions.WebBrowserPermission> <br /> <xref:System.Security.Permissions.WebBrowserPermissionAttribute> <br /> <xref:System.Security.Permissions.WebBrowserPermissionLevel> |
| *System.Xaml.dll* | *System.Security.Permissions.dll* | <xref:System.Xaml.Permissions.XamlLoadPermission> |
| *System.Xaml.dll* | *System.Windows.Extension.dll*    | <xref:System.Xaml.Permissions.XamlAccessLevel><br/> |

> [!NOTE]
> 移植での問題を最小限に抑えるために、次のプロパティに関連する情報を格納および取得するための機能は、`XamlAccessLevel` 型に保持されていました。
>
> - `PrivateAccessToTypeName`
> - `AssemblyNameString`

## <a name="next-steps"></a>次の手順

- [.NET Framework の WPF アプリを .NET Core に移植する方法について学びます。](convert-project-from-net-framework.md)
