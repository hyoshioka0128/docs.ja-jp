---
title: dotnet nuget locals コマンド
description: dotnet nuget locals コマンドは、HTTP 要求キャッシュ、一時的なキャッシュ、コンピューター全体のグローバル パッケージ フォルダーなどのローカルの NuGet リソースをクリアまたは一覧表示します。
author: karann-msft
ms.date: 06/26/2019
ms.openlocfilehash: cb5747636aa9d04f1ef6a6ff9309ba29c0630dd6
ms.sourcegitcommit: 7f8eeef060ddeb2cabfa52843776faf652c5a1f5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74087406"
---
# <a name="dotnet-nuget-locals"></a>dotnet nuget locals

**このトピックの対象: ✓** .NET Core 1.x SDK 以降のバージョン

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>name

`dotnet nuget locals` - ローカル NuGet リソースをクリアまたはリストします。

## <a name="synopsis"></a>構文

```dotnetcli
dotnet nuget locals <CACHE_LOCATION> [(-c|--clear)|(-l|--list)] [--force-english-output]
dotnet nuget locals [-h|--help]
```

## <a name="description"></a>説明

`dotnet nuget locals` コマンドは、HTTP 要求キャッシュ、一時的なキャッシュ、コンピューター全体のグローバル パッケージ フォルダーのローカルの NuGet リソースをクリアまたは一覧表示します。

## <a name="arguments"></a>引数

* **`CACHE_LOCATION`**

  一覧表示またはクリアするキャッシュの場所。 次のいずれかの値を受け入れます。

  * `all` - 指定された操作をすべてのキャッシュの種類 (HTTP 要求キャッシュ、グローバル パッケージ キャッシュ、一時的なキャッシュ) に適用することを指定します。
  * `http-cache` - 指定した操作を HTTP 要求キャッシュのみに適用することを指定します。 その他のキャッシュの場所には影響しません。
  * `global-packages` - 指定した操作をグローバル パッケージ キャッシュのみに適用することを指定します。 その他のキャッシュの場所には影響しません。
  * `temp` - 指定した操作を一時キャッシュのみに適用することを指定します。 その他のキャッシュの場所には影響しません。

## <a name="options"></a>オプション

* **`--force-english-output`**

  インバリアントの英語ベースのカルチャを使用して、アプリケーションの実行を強制します。

* **`-h|--help`**

  コマンドの短いヘルプを印刷します。

* **`-c|--clear`**

  クリア オプションは、指定されたキャッシュの種類でクリア操作を実行します。 キャッシュ ディレクトリの内容は、再帰的に削除されます。 実行中のユーザー/グループには、キャッシュ ディレクトリ内のファイルへのアクセス許可が必要です。 アクセス許可がない場合は、ファイル/フォルダーがクリアされなかったことを示すエラーが表示されます。

* **`-l|--list`**

  一覧表示オプションは、指定されたキャッシュの種類の場所を表示するために使用されます。

## <a name="examples"></a>使用例

* すべてのローカルのキャッシュ ディレクトリ (HTTP キャッシュ ディレクトリ、グローバル パッケージ キャッシュ ディレクトリ、および一時的なキャッシュ ディレクトリ) のパスを表示します。

  ```dotnetcli
  dotnet nuget locals all –l
  ```

* ローカルの HTTP キャッシュ ディレクトリのパスを表示します。

  ```dotnetcli
  dotnet nuget locals http-cache --list
  ```

* すべてのローカルのキャッシュ ディレクトリ (HTTP キャッシュ ディレクトリ、グローバル パッケージ キャッシュ ディレクトリ、および一時的なキャッシュ ディレクトリ) からすべてのファイルをクリアします。

  ```dotnetcli
  dotnet nuget locals all --clear
  ```

* ローカルのグローバル キャッシュ ディレクトリのファイルをすべてクリアします。

  ```dotnetcli
  dotnet nuget locals global-packages -c
  ```

* ローカルの一時的なキャッシュ ディレクトリのファイルをすべてクリアします。

  ```dotnetcli
  dotnet nuget locals temp -c
  ```

## <a name="troubleshooting"></a>トラブルシューティング

`dotnet nuget locals` コマンドを使うときの一般的な問題やエラーについては、「[Managing the NuGet cache](/nuget/consume-packages/managing-the-nuget-cache)」 (NuGet キャッシュを管理する) をご覧ください。
