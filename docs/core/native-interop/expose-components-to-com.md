---
title: COM への .NET Core コンポーネントの公開
description: このチュートリアルでは、.NET Core から COM にクラスを公開する方法について説明します。 COM サーバーと、レジストリを使用しない COM 用のサイドバイサイド サーバー マニフェストを生成します。
ms.date: 07/12/2019
helpviewer_keywords:
- exposing .NET Core components to COM
- interoperation with unmanaged code, exposing .NET Core components
- COM interop, exposing COM components
ms.assetid: 21271167-fe7f-46ba-a81f-a6812ea649d4
author: jkoritzinsky
ms.author: jekoritz
ms.openlocfilehash: 17d85b9e9734fae0bb69f94da8c08669216ab0ae
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81242869"
---
# <a name="exposing-net-core-components-to-com"></a>COM への .NET Core コンポーネントの公開

.NET Core では、.NET Framework と比較し、.NET オブジェクトを COM に公開する工程が大幅に簡素化されています。 次の手順では、クラスを COM に公開する方法について説明します。 このチュートリアルでは、次の方法を紹介します。

- .NET Core から COM にクラスを公開します。
- 使用する .NET Core ライブラリをビルドする一環として、COM サーバーを生成します。
- レジストリを使用しない COM 用の side-by-side サーバー マニフェストを自動生成します。

## <a name="prerequisites"></a>必須コンポーネント

- [NET Core 3.0 SDK](https://dotnet.microsoft.com/download) 以降のバージョンをインストールします。

## <a name="create-the-library"></a>ライブラリを作成する

最初の手順では、ライブラリを作成します。

1. 新しいフォルダーを作成し、そのフォルダーで次のコマンドを実行します。

    ```dotnetcli
    dotnet new classlib
    ```

2. `Class1.cs`を開きます。
3. ファイルの先頭に、`using System.Runtime.InteropServices;` を追加します。
4. `IServer` という名前のインターフェイスを作成します。 次に例を示します。

   ```csharp
   using System;
   using System.Runtime.InteropServices;

   [ComVisible(true)]
   [Guid(ContractGuids.ServerInterface)]
   [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
   public interface IServer
   {
       /// <summary>
       /// Compute the value of the constant Pi.
       /// </summary>
       double ComputePi();
   }
   ```

5. このインターフェイスに、実装する COM インターフェイス用のインターフェイス GUID を使用して、`[Guid("<IID>")]` 属性を追加します。 たとえば、`[Guid("fe103d6e-e71b-414c-80bf-982f18f6c1c7")]` のようにします。 この GUID は、COM 用のこのインターフェイスの唯一の識別子であるため、一意である必要があることに注意してください。 Visual Studio で GUID を作成するには、[ツール] > [GUID の作成] の順に移動して GUI の作成ツールを開きます。
6. インターフェイスに `[InterfaceType]` 属性を追加し、お使いのインターフェイスで実装すべき基本 COM インターフェイスを指定します。
7. `IServer` を実装する、`Server` という名前のクラスを作成します。
8. クラスに、実装する COM クラス用のクラス識別子 GUID を使用して、`[Guid("<CLSID>")]` 属性を追加します。 たとえば、`[Guid("9f35b6f5-2c05-4e7f-93aa-ee087f6e7ab6")]` のようにします。 インターフェイス GUID でこの GUID は、COM ではこのインターフェイスの唯一の識別子であるため、一意である必要があることに注意してください。
9. インターフェイスとクラスの両方に `[ComVisible(true)]` 属性を追加します。

> [!IMPORTANT]
> .NET Framework とは異なり、.NET Core では COM を使用してアクティブ化したいすべてのクラスの CLSID を指定する必要があります。

## <a name="generate-the-com-host"></a>COM ホストを生成する

1. `.csproj` プロジェクト ファイルを開き、`<PropertyGroup></PropertyGroup>` タグの内側に `<EnableComHosting>true</EnableComHosting>` を追加します。
2. プロジェクトをビルドします。

結果として、`ProjectName.dll`、`ProjectName.runtimeconfig.json`、`ProjectName.deps.json`、および`ProjectName.comhost.dll` ファイルが出力されます。

## <a name="register-the-com-host-for-com"></a>COM 用の COM ホストを登録する

管理者特権でのコマンド プロンプトを開き、`regsvr32 ProjectName.comhost.dll` を実行します。 これにより、公開されているすべての .NET オブジェクトが COM に登録されます。

## <a name="enabling-regfree-com"></a>Regfree COM を有効にする

1. `.csproj` プロジェクト ファイルを開き、`<PropertyGroup></PropertyGroup>` タグの内側に `<EnableRegFreeCom>true</EnableRegFreeCom>` を追加します。
2. プロジェクトをビルドします。

これで結果として、`ProjectName.X.manifest` ファイルも出力されます。 このファイルが、Registry-Free COM で使用される side-by-side マニフェストです。

## <a name="sample"></a>サンプル

GitHub の dotnet/samples リポジトリには、完全に機能する [COM サーバーのサンプル](https://github.com/dotnet/samples/tree/master/core/extensions/COMServerDemo)があります。

## <a name="additional-notes"></a>補足メモ

.NET Core では、.NET Framework とは異なり、.NET Core アセンブリからの COM タイプ ライブラリ (TLB) の生成はサポートしていません。 このガイダンスは、COM インターフェイスのネイティブ宣言のために、IDL ファイルまたは C/C++ ヘッダーを手動で記述する方法について説明するものです。

COM コンポーネントの[自己完結型の配置](../deploying/index.md#publish-self-contained)はサポートされていません。 COM コンポーネントの[ランタイムに依存する配置](../deploying/index.md#publish-runtime-dependent)のみがサポートされています。

また、.NET Framework と .NET Core の両方を同じプロセスに読み込むと、診断が制限されます。 主にマネージド コンポーネントのデバッグが制限されます。これは、.NET Framework と .NET Core の両方を同時にデバッグすることはできないためです。 また、2 つのランタイム インスタンスはマネージド アセンブリを共有しません。 つまり、2 つのランタイム間で実際の .NET 型を共有することはできません。代わりに、すべての対話を、公開されている COM インターフェイス コントラクトに制限する必要があります。
