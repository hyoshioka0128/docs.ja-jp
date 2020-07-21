---
title: グローバリゼーションと ICU
ms.date: 05/21/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- globalization [.NET Framework], about globalization
- global applications, globalization
- international applications [.NET Framework], globalization
- world-ready applications, globalization
- application development [.NET Framework], globalization
- culture, globalization
- icu, icu on windows, ms-icu
ms.openlocfilehash: 6ea848d4a60069e6702b9d60fd90a55f572fb043
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842513"
---
# <a name="net-globalization-and-icu"></a>.NET グローバリゼーションと ICU

.NET グローバリゼーション API は、これまで、プラットフォームごとに別の基になるライブラリを使用していました。 この API は、Unix では、[ICU (International Components for Unicode)](http://site.icu-project.org/home) を使用し、Windows では、[各国語サポート (NLS)](/windows/win32/intl/national-language-support) を使用していました。 これにより、アプリケーションを実行するとき、いくつかのグローバリゼーション API の動作がプラットフォームによって違うことがありました。 次の領域で、動作が違うことがわかっています。

- カルチャとカルチャ データ
- 文字の大文字小文字
- 文字の並べ替えと検索
- 並べ替えキー
- 文字の正規化
- 国際化ドメイン名 (IDN) のサポート
- Linux のタイム ゾーンの表示名

.NET 5.0 以降では、プラットフォームによってアプリケーションに違いがでることがないよう、開発者が基になるライブラリをより制御できるようになりました。

## <a name="icu-on-windows"></a>Windows 上の ICU

Windows 10 の 2019 年 5 月更新プログラム以降では、OS の一部として [icu.dll](/windows/win32/intl/international-components-for-unicode--icu-) が含まれるようになり、.NET 5.0 以降のバージョンでは、既定で ICU が使用されるようになりました。 .NET 5.0 以降のバージョンを Windows で実行する場合、`icu.dll` の読み込みが試行され、存在する場合、グローバリゼーションの実装で使用されます。  Windows の古いバージョンを実行している場合などで、このライブラリを見つけたり、読み込むことができない場合、.NET 5.0 以降のバージョンは NLS ベースの実装に戻ります。

> [!NOTE]
> ICU が使用されている場合でも、Windows オペレーティング システム API では、ユーザーが設定している場合は、`CurrentCulture`、`CurrentUICulture`、および `CurrentRegion` のメンバーが使用されます。

### <a name="using-nls-instead-of-icu"></a>ICU の代わりに NLS を使用する

NLS の代わりに ICU を使用すると、一部のグローバリゼーション関連の操作で動作が違ってしまうことがあります。 開発者は、NLS を使用するように、ICU の実装を戻すことを選択することができます。 アプリケーションでは、次のいずれかの方法で NLS モードを有効にできます。

- プロジェクト ファイルで次を実行します。

```xml
<ItemGroup>
  <RuntimeHostConfigurationOption Include="System.Globalization.UseNls" Value="true" />
</ItemGroup>
```

- `runtimeconfig.json` ファイルで次の操作を行います。

```json
{
  "runtimeOptions": {
     "configProperties": {
       "System.Globalization.UseNls": true
      }
  }
}
```

- 環境変数 `DOTNET_SYSTEM_GLOBALIZATION_USENLS` の値を `true` または `1` に設定します。

> [!NOTE]
> プロジェクトまたは `runtimeconfig.json` に設定された値が環境変数に優先されます。

詳細については、[ランタイムの構成設定](../../core/run-time-config/globalization.md#nls)に関するページを参照してください。

## <a name="app-local-icu"></a>アプリローカル ICU

ICU の各リリースには、バグ修正と、世界の言語が記述された更新された共通ロケール データ リポジトリ (CLDR) データが含まれる場合があります。 ICU のバージョンを変えると、グローバリゼーション関連の操作でアプリの動作がわずかに影響を受ける場合があります。  .NET 5.0 以降のバージョンでは、独自の ICU のコピーが Windows と Unix の両方上のアプリに含まれ使用されになっており、アプリケーション開発者が、配置したすべてのアプリで整合性を保てるようになっています。

アプリケーションでは、次のいずれかの方法で、アプリローカル ICU が実装されるモードをオプトインできます。

- プロジェクト ファイルで次の操作を行います。

```xml
<ItemGroup>
  <RuntimeHostConfigurationOption Include="System.Globalization.AppLocalIcu" Value="<suffix>:<version> or <version>" />
</ItemGroup>
```

- `runtimeconfig.json` ファイルで次の操作を行います。

```json
{
  "runtimeOptions": {
     "configProperties": {
       "System.Globalization.AppLocalIcu": "<suffix>:<version> or <version>"
      }
  }
}
```

- 環境変数 `DOTNET_SYSTEM_GLOBALIZATION_APPLOCALICU` の値を `<suffix>:<version>` または `<version>` に設定します。

`<suffix>`:公開されている ICU パッケージ規則に従った、長さが 36 文字未満の省略可能なサフィックス。 ICU をカスタマイズして構築する場合、`libicuucmyapp` のように、ライブラリ名とエクスポートされたシンボル名にサフィックスが含まれるようにカスタマイズできます。ここでは、`myapp` がサフィックスです。

`<version>`:67.1 などの有効な ICU のバージョン。 このバージョンは、バイナリを読み込み、エクスポートされたシンボルを取得するために使用されます。

.NET では、アプリローカルのスイッチが設定されている場合に ICU を読み込むために、複数のパスをプローブする <xref:System.Runtime.InteropServices.NativeLibrary.TryLoad%2A?displayProperty=nameWithType> メソッドが使用されます。 このメソッドでは、まず `NATIVE_DLL_SEARCH_DIRECTORIES` プロパティからライブラリが検索されます。このプロパティは、アプリの `deps.json` ファイルに基づき dotnet ホストが作成します。 詳細については、「[既定のプローブ](../../core/dependency-loading/default-probing.md)」を参照してください。

自己完結型アプリの場合は、ICU がアプリのディレクトリ内にあることを確認する以外に、ユーザーが特別に行う操作はありません (自己完結型アプリの場合、既定の作業ディレクトリは `NATIVE_DLL_SEARCH_DIRECTORIES` です)。

NuGet パッケージの ICU を使用している場合は、フレームワークに依存するアプリケーションでこのようになります。 NuGet はネイティブ資産を解決し、`deps.json` ファイルと `runtimes` ディレクトリ下のアプリケーションの出力ディレクトリにそれを格納します。 .NET はそこからこれを読み込みます。

ローカル ビルドから ICU が使用されるフレームワーク依存のアプリの場合は、手順を追加で実行する必要があります。 .NET SDK には、"ルース" ネイティブ バイナリを `deps.json` に組み込む機能がまだありません ([この SDK の問題](https://github.com/dotnet/sdk/issues/11373)を参照してください)。 代わりに、アプリケーションのプロジェクト ファイルに情報を追加して有効にすることができます。 次に例を示します。

```xml
<ItemGroup>
  <IcuAssemblies Include="icu\*.so*" />
  <RuntimeTargetsCopyLocalItems Include="@(IcuAssemblies)" AssetType="native" CopyLocal="true" DestinationSubDirectory="runtimes/linux-x64/native/" DestinationSubPath="%(FileName)%(Extension)" RuntimeIdentifier="linux-x64" NuGetPackageId="System.Private.Runtime.UnicodeData" />
</ItemGroup>
```

これは、サポートされているランタイムのすべての ICU バイナリに対して実行する必要があります。 また、`RuntimeTargetsCopyLocalItems` 項目グループの `NuGetPackageId` メタデータが、プロジェクトが実際に参照する NuGet パッケージと一致している必要があります。

### <a name="macos-behavior"></a>macOS の動作

`macOS` が `match-o` ファイルで指定した読み込みコマンドから依存しているダイナミック ライブラリを解決する動作は、Linux ローダーの動作とは異なります。 Linux ローダーでは、ICU 依存関係グラフに従い、.NET が `libicudata`、`libicuuc`、および `libicui18n` を (この順序で) 試行します。 ただし、これは macOS では機能しません。 macOS で ICU を構築する場合、ユーザーは既定でこれらの読み込みコマンドで、`libicuuc` にダイナミック ライブラリを取得します。 例を次に示します。

```sh
~/ % otool -L /Users/santifdezm/repos/icu-build/icu/install/lib/libicuuc.67.1.dylib
/Users/santifdezm/repos/icu-build/icu/install/lib/libicuuc.67.1.dylib:
 libicuuc.67.dylib (compatibility version 67.0.0, current version 67.1.0)
 libicudata.67.dylib (compatibility version 67.0.0, current version 67.1.0)
 /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
 /usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
```

これらのコマンドでは、ICU の他のコンポーネントの依存ライブラリの名前のみを参照します。 ローダーは、`dlopen` 表記規則に従って検索を実行します。このとき、これらのライブラリはシステム ディレクトリに配置されているか、`LD_LIBRARY_PATH` 環境変数が設定されているか、アプリレベル ディレクトリに ICU がある必要があります。 `LD_LIBRARY_PATH` を設定できない場合、または ICU バイナリがアプリレベルのディレクトリにない可能性がある場合は、作業を追加で行う必要があります。

ローダーには、その読み込みコマンドでバイナリと同じディレクトリから、その依存関係を検索するように指示する、`@loader_path` などのディレクティブがいくつかあります。 これを実現する方法は 2 つあります。

- `install_name_tool -change`

  次のコマンドを実行します。

```bash
install_name_tool -change "libicudata.67.dylib" "@loader_path/libicudata.67.dylib" /path/to/libicuuc.67.1.dylib
install_name_tool -change "libicudata.67.dylib" "@loader_path/libicudata.67.dylib" /path/to/libicui18n.67.1.dylib
install_name_tool -change "libicuuc.67.dylib" "@loader_path/libicuuc.67.dylib" /path/to/libicui18n.67.1.dylib
```

- `@loader_path` が使用されたインストール名が作成されるよう、ICU をパッチします。

  autoconf (`./runConfigureICU`) を実行する前に、[これらの行](https://github.com/unicode-org/icu/blob/ef91cc3673d69a5e00407cda94f39fcda3131451/icu4c/source/config/mh-darwin#L32-L37)を次のように変更します。

```
LD_SONAME = -Wl,-compatibility_version -Wl,$(SO_TARGET_VERSION_MAJOR) -Wl,-current_version -Wl,$(SO_TARGET_VERSION) -install_name @loader_path/$(notdir $(MIDDLE_SO_TARGET))
```
