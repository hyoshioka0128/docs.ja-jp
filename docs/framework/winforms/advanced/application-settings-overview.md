---
title: アプリケーション設定の概要
description: アプリケーションとユーザーの代わりに設定データを作成して保存する方法など、Windows フォームのアプリケーション設定機能について説明します。
ms.date: 03/30/2017
f1_keywords:
- ApplicationsSettingsOverview
helpviewer_keywords:
- application settings [Windows Forms], about application settings
- dynamic properties
- user preferences [Windows Forms], tracking
ms.assetid: 0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc
ms.openlocfilehash: 864cab72b26ff7989c570347fb88b4009e7d705a
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324218"
---
# <a name="application-settings-overview"></a>アプリケーション設定の概要

この記事では、アプリケーションとユーザーの代わりに設定データを作成して保存する方法について説明します。

 Windows フォームのアプリケーション設定の機能により、カスタム アプリケーションと、クライアント コンピューター上のユーザー設定の作成、保存、および保守が簡単になります。 Windows フォーム アプリケーションの設定ではデータベースの接続文字列など、アプリケーションのデータだけでなく、ユーザー アプリケーションの設定などのユーザー固有のデータを格納することができます。 Visual Studio またはカスタムのマネージド コードを使用して、新しい設定の作成、ディスクからの読み取りまたは書き込み、フォームのプロパティへのバインド、および読み込みと保存の前の設定データの検証を実行することができます。

 アプリケーション設定を使用すると、開発者はカスタムコードをほとんど使用することなく、アプリケーションの状態を保存できます。また、以前のバージョンの .NET Framework では、動的プロパティに代わるものです。 アプリケーション設定には、読み取り専用で、遅延バインディングであり、複数のカスタム プログラミングを必要とする動的プロパティに対する多くの機能強化が含まれます。 動的プロパティクラスは .NET Framework 2.0 で保持されていますが、アプリケーション設定クラスを薄くラップするシェルクラスにすぎません。

## <a name="what-are-application-settings"></a>アプリケーション設定とは何でしょうか?
 Windows フォームアプリケーションでは、多くの場合、アプリケーションの実行に不可欠なデータを必要としますが、アプリケーションのコードに直接含める必要はありません。 アプリケーションで Web サービスまたはデータベースサーバーを使用する場合は、この情報を別のファイルに格納して、再コンパイルせずに後で変更できるようにすることができます。 同様に、アプリケーションは、現在のユーザーに固有の格納データを必要とすることがあります。 たとえば、ほとんどのアプリケーションでは、アプリケーションの外観と動作をカスタマイズするユーザー設定があります。

 アプリケーション設定は、クライアント コンピューターにアプリケーション スコープとユーザー スコープの両方の設定を保存する簡単な方法を提供することにより、両方のニーズに対応します。 Visual Studio またはコード エディターを使用して、名前、データ型、およびスコープ (アプリケーションまたはユーザー) を指定して特定のプロパティの設定を定義します。 使いやすさと読みやすさのために、関連する設定を名前付きのグループに配置することもできます。 これらの設定は、定義された後も保持され、実行時に自動的にメモリに読み込まれます。 プラグ可能なアーキテクチャにより永続化メカニズムを変更できますが、既定では、ローカル ファイル システムが使用されます。

 アプリケーションの設定は、設定がアプリケーション スコープかユーザー スコープかに応じて、別の構成 (.config) ファイルに XML としてデータを保持することで機能します。 ほとんどの場合は、アプリケーション スコープ設定は読み取り専用です。これは、アプリケーション スコープ設定がプログラム情報であり、通常は上書きする必要がないためです。 これに対し、ユーザー スコープ設定は、アプリケーションが部分信頼で実行されている場合でも、実行時に安全に読み書きできます。 部分信頼の詳細については、「 [Security in Windows Forms Overview](../security-in-windows-forms-overview.md)」を参照してください。

 設定は、構成ファイルの XML フラグメントとして格納されます。 アプリケーション スコープ設定は `<applicationSettings>` 要素によって表され、通常は *app*.exe.config に配置されます。ここで、 *app* はメインの実行可能ファイルの名前です。 ユーザー スコープ設定は、 `<userSettings>` 要素によって表され、 *user*.config に配置されます。ここで、 *user* は、現在アプリケーションを実行しているユーザーのユーザー名です。 *app*.exe.config ファイルはアプリケーションと共に展開する必要があります。 *user*.config ファイルは、アプリケーションがそのユーザーの設定を初めて保存するときに、必要に応じて設定アーキテクチャが作成します。 また、 `<userSettings>` app *.exe.config 内で*ブロックを定義して、ユーザー スコープ設定の既定値を指定することもできます。

 カスタム コントロールでは、 <xref:System.Configuration.IPersistComponentSettings> メソッドを公開する <xref:System.Configuration.IPersistComponentSettings.SaveSettings%2A> インターフェイスを実装することで、独自の設定を保存できます。 Windows フォーム <xref:System.Windows.Forms.ToolStrip> コントロールは、このインターフェイスを実装して、アプリケーション セッション間でのツールバーとツールバー項目の位置を保存します。 カスタム コントロールとアプリケーション設定の詳細については、「 [Application Settings for Custom Controls](application-settings-for-custom-controls.md)」を参照してください。

## <a name="limitations-of-application-settings"></a>アプリケーションの設定の制限事項
 .NET Framework をホストするアンマネージアプリケーションでは、アプリケーション設定を使用できません。 Visual Studio アドイン、C++ for Microsoft Office、Internet Explorer のコントロール ホスト、Microsoft Outlook のアドインやプロジェクトなどの環境では、設定は機能しません。

 現在、Windows フォームの一部のプロパティをバインドできません。 最も注目に値する例は、 <xref:System.Windows.Forms.Form.ClientSize%2A> プロパティで、このプロパティへのバインドにより、実行時に予期しない動作が発生します。 これらの設定をプログラムで保存して読み込むことで、通常はこれらの問題を回避できます。

 アプリケーション設定には、情報を自動的に暗号化するための組み込みの機能がありません。 データベースのパスワードなどのセキュリティ関連の情報は、クリア テキストで保存しないでください。 このような機密情報を格納する場合、アプリケーション開発者に、機密情報の安全性を確保する責任があります。 接続文字列を格納する場合は、URL にパスワードをハード コーディングするのではなく、Windows 統合セキュリティを使用することをお勧めします。 詳細については、「 [Code Access Security and ADO.NET](../../data/adonet/code-access-security.md)」を参照してください。

## <a name="getting-started-with-application-settings"></a>アプリケーション設定の概要
 Visual Studio を使用している場合に、Windows フォーム デザイナーの **[プロパティ]** ウィンドウの **(ApplicationSettings)** プロパティを使用して設定を定義することができます。 この方法で設定を定義すると、Visual Studio は、各設定をクラスプロパティに関連付けるカスタムマネージラッパークラスを自動的に作成します。 また、Visual Studio は、フォームが表示されるとコントロールの設定が自動的に復元され、フォームが閉じられると自動的に保存されるように、フォームまたはコントロールのプロパティへの設定のバインドも処理します。

 設定のより詳細なコントロールが必要な場合は、独自のカスタムのアプリケーション設定のラッパー クラスを定義することができます。 これは、 <xref:System.Configuration.ApplicationSettingsBase>からクラスを派生させ、各設定に対応するプロパティを追加して、これらのプロパティに特別な属性を適用することで実現します。 ラッパー クラスを作成する方法については、「 [Application Settings Architecture](application-settings-architecture.md)」を参照してください。

 また、 <xref:System.Windows.Forms.Binding> クラスを使用して、フォームとコントロールのプロパティに設定をプログラムでバインドすることもできます。

## <a name="see-also"></a>関連項目

- <xref:System.Configuration.ApplicationSettingsBase>
- <xref:System.Configuration.SettingsProvider>
- <xref:System.Configuration.LocalFileSettingsProvider>
- <xref:System.Configuration.IPersistComponentSettings>
- [方法: アプリケーション設定を検証する](how-to-validate-application-settings.md)
- [アプリケーションの設定の管理 (.NET)](/visualstudio/ide/managing-application-settings-dotnet)
- [方法: 実行時に設定を C# で読み取る](how-to-read-settings-at-run-time-with-csharp.md)
- [アプリケーション設定とユーザー設定の使用](using-application-settings-and-user-settings.md)
- [アプリケーション設定アーキテクチャ](application-settings-architecture.md)
- [カスタム コントロールのアプリケーション設定](application-settings-for-custom-controls.md)
