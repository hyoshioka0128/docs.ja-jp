---
title: アンマネージド ライブラリの読み込みアルゴリズム - .NET Core
description: .NET Core でのアンマネージド アセンブリ読み込みアルゴリズムの詳細の説明
ms.date: 10/09/2019
author: sdmaclea
ms.author: stmaclea
ms.openlocfilehash: c651aa6e0f37a968e6f8b26d1909def6fa488ccd
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "72303696"
---
# <a name="unmanaged-native-library-loading-algorithm"></a>アンマネージド (ネイティブ) ライブラリの読み込みアルゴリズム

アンマネージド ライブラリは、さまざまな段階を伴うアルゴリズムを使用して検出され、読み込まれます。

次のアルゴリズムでは、`PInvoke` によってネイティブ ライブラリがどのように読み込まれるかを説明します。

## <a name="pinvoke-load-library-algorithm"></a>`PInvoke` のライブラリ読み込みアルゴリズム

`PInvoke` では、アンマネージド アセンブリを読み込むときに、次のアルゴリズムが使用されます。

1. `active` <xref:System.Runtime.Loader.AssemblyLoadContext> を決定します。 アンマネージド ライブラリ読み込みの場合、`active` AssemblyLoadContext が、`PInvoke` を定義するアセンブリを持っています。

2. `active` <xref:System.Runtime.Loader.AssemblyLoadContext> について、次の優先順位に従ってアセンブリを検索します。
    * キャッシュを調べます。

    * <xref:System.Runtime.InteropServices.NativeLibrary.SetDllImportResolver(System.Reflection.Assembly,System.Runtime.InteropServices.DllImportResolver)?displayProperty=nameWithType> 関数によって設定された現在の <xref:System.Runtime.InteropServices.DllImportResolver?displayProperty=nameWithType> デリゲートを呼び出します。

    * `active` AssemblyLoadContext で <xref:System.Runtime.Loader.AssemblyLoadContext.LoadUnmanagedDll%2A?displayProperty=nameWithType> 関数を呼び出します。

    * <xref:System.AppDomain> インスタンスのキャッシュを確認し、[アンマネージ (ネイティブ) ライブラリプローブ](default-probing.md#unmanaged-native-library-probing) ロジックを実行します。

    * `active` AssemblyLoadContext の <xref:System.Runtime.Loader.AssemblyLoadContext.ResolvingUnmanagedDll?displayProperty=nameWithType> イベントを発生させます。
