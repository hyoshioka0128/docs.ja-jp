---
title: '方法: グローバル アセンブリ キャッシュの内容を表示する'
description: グローバル アセンブリ キャッシュ (GAC) ツール (gacutil.exe) を使用して .NET でグローバル アセンブリ キャッシュの内容を表示する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- global assembly cache, viewing contents
- viewing assemblies in global assembly cache
- Gacutil.exe
- strong-named assemblies, global assembly cache
- GAC (global assembly cache), viewing contents
- list of assemblies in global assembly cache
- Global Assembly Cache tool
ms.assetid: c5f786a0-969b-4f14-9f02-e77c3384d9af
ms.openlocfilehash: 4d775efc073f3aad745eff7a7707efdec06172c2
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85104689"
---
# <a name="how-to-view-the-contents-of-the-global-assembly-cache"></a>方法: グローバル アセンブリ キャッシュの内容を表示する

[グローバル アセンブリ キャッシュ ツール (gacutil.exe)](../tools/gacutil-exe-gac-tool.md) を使用して、グローバル アセンブリ キャッシュ (GAC) の内容を表示できます。

## <a name="view-the-assemblies-in-the-gac"></a>GAC 内のアセンブリを表示する

グローバル アセンブリ キャッシュ内のアセンブリの一覧を表示するには、[Visual Studio 用開発者コマンド プロンプト](../tools/developer-command-prompt-for-vs.md)を開いて次のコマンドを入力します。

```shell
gacutil -l
```

\- または -

```shell
gacutil /l
```

> [!NOTE]
> 以前のバージョンの .NET Framework では、Windows のシェル拡張機能である [Shfusion.dll](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/34149zk3(v=vs.100)) により、エクスプローラーでグローバル アセンブリ キャッシュを表示することができました。 .NET Framework 4 以降、Shfusion.dll は廃止されましたが、互換性のために残されています。

## <a name="see-also"></a>関連項目

- [アセンブリとグローバル アセンブリ キャッシュの使用](working-with-assemblies-and-the-gac.md)
- [Gacutil.exe (グローバル アセンブリ キャッシュ ツール)](../tools/gacutil-exe-gac-tool.md)
