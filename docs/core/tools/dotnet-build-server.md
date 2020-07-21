---
title: dotnet build-server コマンド
description: dotnet build-server コマンドは、ビルドによって起動されたサーバーとやり取りします。
ms.date: 02/14/2020
ms.openlocfilehash: 882b697c07aac0e20266f3ad4e6c11888a0b7acc
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463722"
---
# <a name="dotnet-build-server"></a>dotnet build-server

**この記事の対象:** ✔️ .NET Core 2.1 SDK 以降のバージョン

## <a name="name"></a>name

`dotnet build-server` - ビルドによって起動されたサーバーとやり取りします。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet build-server shutdown [--msbuild] [--razor] [--vbcscompiler]

dotnet build-server shutdown -h|--help

dotnet build-server -h|--help
```

## <a name="commands"></a>コマンド

- **`shutdown`**

  dotnet から起動されるビルド サーバーをシャットダウンします。 既定では、すべてのサーバーがシャットダウンされます。

## <a name="options"></a>オプション

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

- **`--msbuild`**

  MSBuild ビルド サーバーをシャットダウンします。

- **`--razor`**

  Razor ビルド サーバーをシャットダウンします。

- **`--vbcscompiler`**

  VB/C# コンパイラ ビルド サーバーをシャットダウンします。
