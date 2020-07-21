---
title: dotnet help コマンド
description: dotnet help コマンドでは、指定したコマンドについてより詳細なドキュメントがオンラインで表示されます。
ms.date: 02/14/2020
ms.openlocfilehash: a59e74a318118b6fd39d1895df02d76daa6fc9e1
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463692"
---
# <a name="dotnet-help-reference"></a>dotnet help リファレンス

**この記事の対象:** ✔️ .NET Core 2.0 SDK 以降のバージョン

## <a name="name"></a>name

`dotnet help` - 指定したコマンドについて、より詳細なドキュメントがオンラインで表示されます。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet help <COMMAND_NAME> [-h|--help]
```

## <a name="description"></a>[説明]

`dotnet help` コマンドは、docs.microsoft.com で、指定したコマンドに関する詳細情報のリファレンス ページを開きます。

## <a name="arguments"></a>引数

- **`COMMAND_NAME`**

  .NET Core CLI コマンドの名前です。 有効な CLI コマンドの一覧については、[CLI コマンド](index.md#cli-commands)を参照してください。

## <a name="options"></a>オプション

- **`-h|--help`**

  コマンドの短いヘルプを印刷します。

## <a name="examples"></a>例

- ドキュメントの [dotnet new](dotnet-new.md) コマンドに関するページを開きます。

  ```dotnetcli
  dotnet help new
  ```
