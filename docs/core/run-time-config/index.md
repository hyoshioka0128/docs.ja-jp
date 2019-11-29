---
title: ランタイムの構成
description: ランタイム構成設定を使用して .NET Core アプリケーションを構成する方法について説明します。
ms.date: 11/13/2019
ms.openlocfilehash: f7074b07bdd5aca23b6caae78952d630d905c489
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283964"
---
# <a name="net-core-run-time-configuration-settings"></a>.NET Core ランタイム構成設定

.NET Core では、実行時に .NET Core アプリケーションの動作を構成するために、構成ファイルと環境変数の使用がサポートされています。 ランタイムの構成は、次の場合に適しています。

- アプリケーションのソースコードを所有または制御していないため、プログラムで構成することができない。

- アプリケーションの複数のインスタンスが 1 つのシステムで同時に実行され、最適なパフォーマンスを実現するために各インスタンスを構成する必要がある。

> [!NOTE]
> このドキュメントは現在作成中です。 ここに記載されている情報が不完全であるか、不正確であることがわかった場合は、[イシューを作成](https://github.com/dotnet/docs/issues)してお知らせになるか、[pull request を送信](https://github.com/dotnet/docs/pulls)してイシューに対処してください。 dotnet/docs リポジトリに対する pull request の送信については、[共同作成者のガイド](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md)を参照してください。

.NET Core には、実行時にアプリケーションを構成するための次のメカニズムが用意されています。

- [runtimeconfig.json ファイル](#runtimeconfigjson)

- [環境変数](#environment-variables)

ドキュメントのこのセクションの記事は、デバッグやガベージ コレクションなどのカテゴリ別に分類されています。 *runtimeconfig. json* (.NET Core のみ)、*app.config* (.NET Framework のみ)、および環境変数で使用可能な構成オプションが示されています。

## <a name="runtimeconfigjson"></a>runtimeconfig.json

*runtimeconfig.json* ファイルの **configProperties** セクションで、ランタイム構成オプションを指定します。 このセクションには次の形式が含まれます。

```json
{
   "runtimeOptions": {
      "configProperties": {
         "config-property-name1": "config-value1",
         "config-property-name2": "config-value2"
      }
   }
}
```

ファイルの例を次に示します。

```json
{
   "runtimeOptions": {
      "configProperties": {
         "System.GC.Concurrent": true,
         "System.GC.RetainVM": true,
         "System.Threading.ThreadPool.MinThreads": "4",
         "System.Threading.ThreadPool.MaxThreads": "25"
      }
   }
}
```

*runtimeconfig. json* ファイルは、[dotnet build](../tools/dotnet-build.md) コマンドによってビルド ディレクトリに自動的に作成されます。 また、Visual Studio で **[ビルド]** メニュー オプションを選択したときにも作成されます。 ファイルが作成されたら、編集できます。

一部の構成値は、<xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> メソッドを呼び出すことによって、プログラムで設定することもできます。

## <a name="environment-variables"></a>環境変数

環境変数を使用すると、ランタイムの構成情報を指定できます。 環境変数として指定された構成ノブには、一般に **COMPlus_** のプレフィックスが付いています。

環境変数は、Windows のコントロール パネル、コマンド ライン、または Windows と Unix ベースのシステムの両方で <xref:System.Environment.SetEnvironmentVariable(System.String,System.String)?displayProperty=nameWithType> メソッドを呼び出すことによって、プログラムで定義できます。

次の例は、コマンド ラインで環境変数を設定する方法を示しています。

```shell
# Windows
set COMPlus_GCRetainVM=1

# Powershell
$env:COMPlus_GCRetainVM="1"

# Unix
export COMPlus_GCRetainVM=1
```
