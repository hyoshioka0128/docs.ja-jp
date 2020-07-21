---
title: アプリケーション設定アーキテクチャ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application settings [Windows Forms], architecture
ms.assetid: c8eb2ad0-fac6-4ea2-9140-675a4a44d562
ms.openlocfilehash: 078b5f3fc1cd4273af282580f41e68ca9bd8ff51
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182622"
---
# <a name="application-settings-architecture"></a>アプリケーション設定アーキテクチャ
このトピックでは、アプリケーション設定アーキテクチャのしくみについて説明します。また、グループ化された設定や設定キーなど、アーキテクチャの高度な機能についても説明します。

 アプリケーション設定アーキテクチャでは、アプリケーション スコープまたはユーザー スコープで厳密に型指定された設定の定義と、アプリケーション セッション間での設定の永続化をサポートします。 このアーキテクチャは、ローカル ファイル システムに設定を保存し、ローカル ファイル システムから設定を読み込むための既定の永続化エンジンを提供します。 また、カスタム永続化エンジンを指定するためのインターフェイスも定義します。

 アプリケーションでカスタム コンポーネントがホストされているときに、そのコンポーネントの独自の設定を永続化できるようにするインターフェイスが提供されます。 設定キーを使用することで、各コンポーネントはそのコンポーネントの複数のインスタンスの設定を区別できます。

## <a name="defining-settings"></a>設定の定義
 アプリケーション設定アーキテクチャは、ASP.NETと Windows フォームの両方で使用され、両方の環境で共有される多くの基本クラスが含まれています。 最も重要なのは<xref:System.Configuration.SettingsBase>、コレクションを通じて設定にアクセスし、設定を読み込みおよび保存するための低レベルのメソッドを提供する です。 各環境は、その環境に追加の<xref:System.Configuration.SettingsBase>設定機能を提供するために派生した独自のクラスを実装します。 Windows フォーム ベースのアプリケーションでは、すべてのアプリケーション設定を<xref:System.Configuration.ApplicationSettingsBase>クラスから派生したクラスで定義する必要があります。

- 上位レベルの読み込み操作と保存操作

- ユーザー スコープの設定のサポート

- ユーザーの設定を定義済みの既定値に戻す機能

- 以前のバージョンのアプリケーションの設定のアップグレード

- 設定の変更前または保存前の検証

 設定は、名前空間内で定義された属性の数を<xref:System.Configuration>使用して記述できます。これらの説明については、「[アプリケーション設定の属性](application-settings-attributes.md)」を参照してください。 設定を定義する場合は、アプリケーション全体に適用するか<xref:System.Configuration.ApplicationScopedSettingAttribute>、<xref:System.Configuration.UserScopedSettingAttribute>現在のユーザーだけに適用するかを示す いずれかまたはを使用して設定を適用する必要があります。

 次のコード例では、`BackgroundColor` という 1 つの設定を指定してカスタム設定クラスを定義しています。

 [!code-csharp[ApplicationSettings.Create#1](~/samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/MyAppSettings.cs#1)]
 [!code-vb[ApplicationSettings.Create#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/MyAppSettings.vb#1)]

## <a name="settings-persistence"></a>設定の永続化
 クラス<xref:System.Configuration.ApplicationSettingsBase>自体は設定を保持または読み込みしません。このジョブは、設定プロバイダ (から派生したクラス)<xref:System.Configuration.SettingsProvider>に分類されます。 派生クラスが<xref:System.Configuration.ApplicationSettingsBase><xref:System.Configuration.SettingsProviderAttribute>を使用して設定プロバイダを指定しない場合は、既定のプロバイダ<xref:System.Configuration.LocalFileSettingsProvider>が使用されます。

 .NET Framework で最初にリリースされた構成システムでは、ローカル コンピューターの machine.config ファイルを使用するか、アプリケーションと共に`app.`配置する exe.config ファイルを使用して、静的なアプリケーション構成データを提供できます。 この<xref:System.Configuration.LocalFileSettingsProvider>クラスは、次の方法でこのネイティブ サポートを拡張します。

- アプリケーション スコープの設定は、machine.config ファイルまたは `app.`exe.config ファイルに保存できます。 machine.config は常に読み取り専用です。`app`.exe.config は、セキュリティを考慮して、ほとんどのアプリケーションで読み取り専用に制限されています。

- ユーザー スコープの設定は、`app`.exe.config ファイルに保存できます。この場合、設定は静的な既定値として扱われます。

- 既定値以外のユーザー スコープの設定は、*user*.config という新しいファイルに保存されます。*user* は、アプリケーションを現在実行しているユーザーのユーザー名です。 ユーザー スコープの設定の既定値は、 で<xref:System.Configuration.DefaultSettingValueAttribute>指定できます。 ユーザー スコープの設定はアプリケーションの実行時に変更されることが多いため、`user`.config は常に読み取り/書き込みになります。

 この 3 つの構成ファイルはいずれも XML 形式で設定を保存します。 アプリケーション スコープの設定の最上位の XML 要素は `<appSettings>` であり、ユーザー スコープの設定には `<userSettings>` が使用されます。 アプリケーション スコープの設定と、ユーザー スコープの設定の既定値が含まれた `app`.exe.config ファイルは、次のようになります。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <configSections>
        <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >
            <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
        </sectionGroup>
        <sectionGroup name="userSettings" type="System.Configuration.UserSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >
            <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" />
        </sectionGroup>
    </configSections>
    <applicationSettings>
        <WindowsApplication1.Properties.Settings>
            <setting name="Cursor" serializeAs="String">
                <value>Default</value>
            </setting>
            <setting name="DoubleBuffering" serializeAs="String">
                <value>False</value>
            </setting>
        </WindowsApplication1.Properties.Settings>
    </applicationSettings>
    <userSettings>
        <WindowsApplication1.Properties.Settings>
            <setting name="FormTitle" serializeAs="String">
                <value>Form1</value>
            </setting>
            <setting name="FormSize" serializeAs="String">
                <value>595, 536</value>
            </setting>
        </WindowsApplication1.Properties.Settings>
    </userSettings>
</configuration>
```

 構成ファイルのアプリケーション設定セクション内の要素の定義については、「[アプリケーション設定のスキーマ](../../configure-apps/file-schema/application-settings-schema.md)」を参照してください。

### <a name="settings-bindings"></a>設定のバインド
 アプリケーション設定では、Windows フォーム データ バインド アーキテクチャを使用して、設定オブジェクトとコンポーネント間で設定の更新の双方向通信を行います。 Visual Studio を使用してアプリケーション設定を作成し、設定をコンポーネントのプロパティに割り当てると、これらのバインドが自動的に生成されます。

 アプリケーション設定は、<xref:System.Windows.Forms.IBindableComponent>そのインターフェイスをサポートするコンポーネントにのみバインドできます。 また、コンポーネントは、特定のバインドされたプロパティの変更イベントを実装するか、インターフェイスを通じてプロパティが変更されたことをアプリケーション<xref:System.ComponentModel.INotifyPropertyChanged>設定に通知する必要があります。 コンポーネントが実装<xref:System.Windows.Forms.IBindableComponent>されず、Visual Studio を使用してバインドする場合、バインドされたプロパティは最初に設定されますが、更新されません。 コンポーネントが実装<xref:System.Windows.Forms.IBindableComponent>しているがプロパティ変更通知をサポートしていない場合、プロパティが変更されたときに、設定ファイル内のバインドは更新されません。

 などの<xref:System.Windows.Forms.ToolStripItem>Windows フォーム コンポーネントの中には、設定バインドをサポートしていないものがあります。

### <a name="settings-serialization"></a>設定のシリアル化
 設定<xref:System.Configuration.LocalFileSettingsProvider>をディスクに保存する必要がある場合、次の操作を実行します。

1. リフレクションを使用して、派生クラスで定義<xref:System.Configuration.ApplicationSettingsBase>されているすべてのプロパティを調べ、いずれか<xref:System.Configuration.UserScopedSettingAttribute>または を<xref:System.Configuration.ApplicationScopedSettingAttribute>使用して適用されたプロパティを見つける。

2. プロパティをディスクにシリアル化します。 まず、型の関連付けられた<xref:System.ComponentModel.TypeConverter.ConvertToString%2A><xref:System.ComponentModel.TypeConverter><xref:System.ComponentModel.TypeConverter.ConvertFromString%2A>の を 呼び出そうとします。 この呼び出しが失敗すると、代わりに XML シリアル化を使用します。

3. 設定の属性に基づいて、どの設定がどのファイルに指定されているかを判断します。

 独自の設定クラスを実装する場合は、 を<xref:System.Configuration.SettingsSerializeAsAttribute>使用して、列挙体を使用してバイナリシリアル化または<xref:System.Configuration.SettingsSerializeAs>カスタム シリアル化のいずれかの設定をマークできます。 コードで独自の設定クラスを作成する方法の詳細については、「[方法 : アプリケーション設定を作成する](how-to-create-application-settings.md)」を参照してください。

### <a name="settings-file-locations"></a>設定ファイルの場所
 `app`.exe.config ファイルと *user*.config ファイルの場所は、アプリケーションのインストール方法によって異なります。 ローカル コンピュータにコピーされた Windows フォーム ベースのアプリケーションの`app`場合、.exe.config はアプリケーションのメイン実行可能ファイルのベース ディレクトリと同じディレクトリに格納され、*ユーザー*.config はプロパティで指定された<xref:System.Windows.Forms.Application.LocalUserAppDataPath%2A?displayProperty=nameWithType>場所に格納されます。 ClickOnce を使用してインストールされたアプリケーションの場合、これらのファイルはどちらも%InstallRoot%\ドキュメントと設定\\*ユーザー名*\ローカル設定の下の ClickOnce データ ディレクトリに格納されます。

 ユーザーが移動プロファイルを有効にしている場合、これらのファイルの格納場所は若干異なります。 その場合、ClickOnce アプリケーションと非 ClickOnce アプリケーションの両方が`app`、.exe.config ファイルと*ユーザー*.config ファイルを %InstallRoot%\ドキュメントおよび設定\\*ユーザー名*\アプリケーション データの下に格納します。

 アプリケーション設定機能と新しい配置テクノロジの連携の詳細については、「[ClickOnce とアプリケーション設定](/visualstudio/deployment/clickonce-and-application-settings)」を参照してください。 ClickOnce データ ディレクトリの詳細については、「 [ClickOnce アプリケーションでローカル データとリモート データにアクセスする](/visualstudio/deployment/accessing-local-and-remote-data-in-clickonce-applications)」を参照してください。

## <a name="application-settings-and-security"></a>アプリケーション設定とセキュリティ
 アプリケーション設定は部分信頼で機能するように設計されています。部分信頼は、インターネットまたはイントラネット上でホストされる Windows フォーム アプリケーションの既定の制限された環境です。 既定の設定プロバイダーでアプリケーション設定を使用する場合、部分信頼以外の特別なアクセス許可は不要です。

 アプリケーション設定が ClickOnce アプリケーションで使用されている場合`user`、.config ファイルは ClickOnce データ ディレクトリに格納されます。 アプリケーションの .config ファイル`user`のサイズは、ClickOnce によって設定されたデータ ディレクトリ クォータを超えることはできません。 詳細については、「[ClickOnce とアプリケーション設定](/visualstudio/deployment/clickonce-and-application-settings)」を参照してください。

## <a name="custom-settings-providers"></a>カスタム設定プロバイダー
 アプリケーション設定アーキテクチャでは、 から派生したアプリケーション設定ラッパー クラスと、 から<xref:System.Configuration.ApplicationSettingsBase>派生した設定プロバイダ (1 つまたは 2 つ以上<xref:System.Configuration.SettingsProvider>) の間に疎結合があります。 この関連付けは、ラッパー<xref:System.Configuration.SettingsProviderAttribute>クラスまたはその個々のプロパティに適用されるによって定義されます。 設定プロバイダーが明示的に指定されていない場合は、既定のプロバイダー<xref:System.Configuration.LocalFileSettingsProvider>が使用されます。 そのため、このアーキテクチャではカスタム設定プロバイダーの作成と使用がサポートされています。

 たとえば、すべての設定データを Microsoft SQL Server データベースに格納するプロバイダーである `SqlSettingsProvider` を開発して使用するとします。 派生<xref:System.Configuration.SettingsProvider>クラスは、この情報を`Initialize`メソッド内で type<xref:System.Collections.Specialized.NameValueCollection?displayProperty=nameWithType>のパラメーターとして受け取ります。 その後、データ<xref:System.Configuration.SettingsProvider.GetPropertyValues%2A>ストアから設定を取得し<xref:System.Configuration.SettingsProvider.SetPropertyValues%2A>、保存するメソッドを実装します。 提供<xref:System.Configuration.SettingsPropertyCollection>された を<xref:System.Configuration.SettingsProvider.GetPropertyValues%2A>使用して、プロパティの名前、型、スコープ、およびそのプロパティに定義されているその他の設定属性を決定できます。

 カスタム プロバイダーでは、1 つのプロパティと 1 つのメソッドを実装する必要がありますが、この実装はわかりにくいことがあります。 プロパティ<xref:System.Configuration.SettingsProvider.ApplicationName%2A>は、<xref:System.Configuration.SettingsProvider>の抽象プロパティです。次の値を返すようにプログラムする必要があります。

 [!code-csharp[ApplicationSettings.Architecture#2](~/samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Architecture/CS/DummyClass.cs#2)]
 [!code-vb[ApplicationSettings.Architecture#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Architecture/VB/DummyProviderClass.vb#2)]

 派生クラスでは、引数を受け取らず値を返さない `Initialize` メソッドも実装する必要があります。 このメソッドは、 で<xref:System.Configuration.SettingsProvider>定義されていません。

 最後に、プロバイダー<xref:System.Configuration.IApplicationSettingsProvider>を実装して、設定の更新、設定の既定値への戻し、アプリケーションバージョン間の設定のアップグレードをサポートします。

 カスタム プロバイダーを実装してコンパイルしたら、既定のプロバイダーではなく、このプロバイダーを使用するよう設定クラスに指示する必要があります。 これは、 を通<xref:System.Configuration.SettingsProviderAttribute>じて実行されます。 設定クラス全体に適用すると、プロバイダはクラスが定義する各設定に対して使用されます。個々の設定に適用した場合、アプリケーション設定アーキテクチャは、そのプロバイダーをそれらの設定にのみ<xref:System.Configuration.LocalFileSettingsProvider>使用し、残りの設定を使用します。 次のコード例は、カスタム プロバイダーを使用するよう設定クラスに指示する方法を示しています。

 [!code-csharp[ApplicationSettings.Architecture#1](~/samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Architecture/CS/DummyClass.cs#1)]
 [!code-vb[ApplicationSettings.Architecture#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Architecture/VB/DummyProviderClass.vb#1)]

 プロバイダーを複数のスレッドから同時に呼び出すことができますが、プロバイダーは常に同じ格納場所に書き込みを行います。したがって、アプリケーション設定アーキテクチャによってインスタンス化されるカスタム プロバイダー クラスのインスタンスは 1 つに限られます。

> [!IMPORTANT]
> カスタム プロバイダーがスレッドセーフであり、構成ファイルへの書き込みを実行できるスレッドが一度に 1 つだけであることを確認する必要があります。

 プロバイダは、名前空間で定義されているすべての<xref:System.Configuration?displayProperty=nameWithType>設定属性をサポートする必要<xref:System.Configuration.ApplicationScopedSettingAttribute><xref:System.Configuration.UserScopedSettingAttribute><xref:System.Configuration.DefaultSettingValueAttribute>はありません。 サポートされていない属性がある場合、カスタム プロバイダーは通知なしに失敗します。例外をスローする必要はありません。 ただし、設定クラスが無効な属性の組み合わせを使用している場合<xref:System.Configuration.ApplicationScopedSettingAttribute>(<xref:System.Configuration.UserScopedSettingAttribute>同じ設定の適用や設定など)、プロバイダは例外をスローして操作を中止する必要があります。

## <a name="see-also"></a>関連項目

- <xref:System.Configuration.ApplicationSettingsBase>
- <xref:System.Configuration.SettingsProvider>
- <xref:System.Configuration.LocalFileSettingsProvider>
- [アプリケーション設定の概要](application-settings-overview.md)
- [カスタム コントロールのアプリケーション設定](application-settings-for-custom-controls.md)
- [クリックワンスとアプリケーション設定](/visualstudio/deployment/clickonce-and-application-settings)
- [アプリケーション設定スキーマ](../../configure-apps/file-schema/application-settings-schema.md)
