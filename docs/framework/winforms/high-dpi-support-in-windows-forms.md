---
title: 高 DPI サポート
description: 一般的な高 DPI および動的 DPI シナリオでの Windows フォームのサポートについて説明します。 また、高 DPI サポート用に Windows フォームアプリケーションを構成する方法についても説明します。
ms.date: 05/16/2017
helpviewer_keywords:
- High DPI in Windows Forms
- Dynamic rescaling in Windows Forms
- Windows Forms layout
- Windows Forms dynamic resizing
ms.assetid: 075ea4c3-900c-4f8a-9dd2-13ea6804346b
ms.openlocfilehash: a9e0766307095da447c772de5a3065c18b7b7154
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325651"
---
# <a name="high-dpi-support-in-windows-forms"></a>Windows フォームでの高 DPI サポート

.NET Framework 4.7 以降の Windows フォームには、一般的な高 DPI および動的 DPI シナリオの機能強化が含まれています。 次の設定があります。

- コントロールやコントロールなど、多数の Windows フォームコントロールのスケーリングとレイアウトの機能強化 <xref:System.Windows.Forms.MonthCalendar> <xref:System.Windows.Forms.CheckedListBox> 。

- シングルパススケーリング。  .NET Framework 4.6 以前のバージョンでは、複数のパスによってスケーリングが実行され、いくつかのコントロールが必要以上に拡大縮小されました。

- Windows フォームアプリケーションの起動後にユーザーが DPI またはスケールファクターを変更する動的な DPI シナリオのサポート。

.NET Framework 4.7 以降の .NET Framework のバージョンでは、強化された高 DPI サポートはオプトイン機能です。 アプリケーションを利用するように構成する必要があります。

## <a name="configuring-your-windows-forms-app-for-high-dpi-support"></a>高 DPI サポート用の Windows フォームアプリの構成

高 DPI 認識をサポートする新しい Windows フォーム機能は、.NET Framework 4.7 を対象とし、Windows 10 の作成者の更新プログラム以降で Windows オペレーティングシステムで実行されているアプリケーションでのみ使用できます。

さらに、Windows フォームアプリケーションで高 DPI サポートを構成するには、次の操作を行う必要があります。

- Windows 10 との互換性を宣言します。

  これを行うには、マニフェストファイルに次のを追加します。

  ```xml
  <compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1">
    <application>
      <!-- Windows 10 compatibility -->
      <supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
    </application>
  </compatibility>
  ```

- *app.config*ファイルでモニターごとの DPI 認識を有効にします。

  Windows フォーム [`<System.Windows.Forms.ApplicationConfigurationSection>`](../configure-apps/file-schema/winforms/index.md) では、.NET Framework 4.7 以降に追加された新しい機能とカスタマイズをサポートする新しい要素が導入されています。 高 DPI をサポートする新機能を利用するには、アプリケーション構成ファイルに次の内容を追加します。

  ```xml
  <System.Windows.Forms.ApplicationConfigurationSection>
    <add key="DpiAwareness" value="PerMonitorV2" />
  </System.Windows.Forms.ApplicationConfigurationSection>
  ```

  > [!IMPORTANT]
  > 以前のバージョンの .NET Framework では、マニフェストを使用して高 DPI サポートを追加していました。 app.config ファイルで定義されている設定を上書きするため、この方法は推奨されなくなりました。

- 静的メソッドを呼び出し <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> ます。

  これは、アプリケーションのエントリポイントの最初のメソッド呼び出しである必要があります。 次に例を示します。

  ```csharp
  static void Main()
  {
      Application.EnableVisualStyles();
      Application.SetCompatibleTextRenderingDefault(false);
      Application.Run(new Form2());
  }
  ```

## <a name="opting-out-of-individual-high-dpi-features"></a>個々の高 DPI 機能のオプトアウト

`DpiAwareness`値をに設定 `PerMonitorV2` すると、.NET Framework 4.7 以降の .NET Framework バージョンでサポートされているすべての高 DPI 認識機能が有効になります。 通常、これはほとんどの Windows フォームアプリケーションに適しています。 ただし、1つまたは複数の個別の機能を無効にすることもできます。 これを行う最も重要な理由は、既存のアプリケーションコードで既にその機能が処理されていることです。  たとえば、アプリケーションで自動スケーリングを処理する場合は、次のように自動サイズ変更機能を無効にすることをお勧めします。

```xml
<System.Windows.Forms.ApplicationConfigurationSection>
  <add key="DpiAwareness" value="PerMonitorV2" />
  <add key="EnableWindowsFormsHighDpiAutoResizing" value="false" />
</System.Windows.Forms.ApplicationConfigurationSection>
```

個々のキーとその値の一覧については、「 [Windows フォーム Add Configuration 要素](../configure-apps/file-schema/winforms/windows-forms-add-configuration-element.md)」を参照してください。

## <a name="new-dpi-change-events"></a>新しい DPI 変更イベント

.NET Framework 4.7 以降では、次の3つの新しいイベントを使用して、動的な DPI 変更をプログラムで処理できます。

- <xref:System.Windows.Forms.Control.DpiChangedAfterParent>。親コントロールまたはフォームの DPI 変更イベントが発生した後に、コントロールの DPI 設定がプログラムによって変更されたときに発生します。
- <xref:System.Windows.Forms.Control.DpiChangedBeforeParent>。親コントロールまたはフォームの DPI 変更イベントが発生する前に、コントロールの DPI 設定がプログラムによって変更されたときに発生します。
- <xref:System.Windows.Forms.Form.DpiChanged>。フォームが現在表示されているディスプレイデバイスで DPI 設定が変更されたときに発生します。

## <a name="new-helper-methods-and-properties"></a>新しいヘルパーメソッドとプロパティ

また、.NET Framework 4.7 では、DPI スケーリングに関する情報を提供し、DPI スケーリングを実行できる新しいヘルパーメソッドとプロパティが多数追加されています。 次の設定があります。

- <xref:System.Windows.Forms.Control.LogicalToDeviceUnits%2A>。値を論理ピクセルからデバイスピクセルに変換します。

- <xref:System.Windows.Forms.Control.ScaleBitmapLogicalToDevice%2A>。ビットマップイメージをデバイスの論理 DPI にスケーリングします。

- <xref:System.Windows.Forms.Control.DeviceDpi%2A>。現在のデバイスの DPI を返します。

## <a name="versioning-considerations"></a>バージョン管理に関する考慮事項

.NET Framework 4.7 と Windows 10 の作成者の更新プログラムで実行するだけでなく、アプリケーションも高 DPI の機能強化と互換性のない環境で実行される場合があります。 この場合、アプリケーションのフォールバックを開発する必要があります。 これを行うと、スケーリングを処理する[カスタム描画](./controls/user-drawn-controls.md)を実行できます。

これを行うには、アプリが実行されているオペレーティングシステムを特定する必要もあります。 そのためには、次のようなコードを使用します。

```csharp
// Create a reference to the OS version of Windows 10 Creators Update.
Version OsMinVersion = new Version(10, 0, 15063, 0);

// Access the platform/version of the current OS.
Console.WriteLine(Environment.OSVersion.Platform.ToString());
Console.WriteLine(Environment.OSVersion.VersionString);

// Compare the current version to the minimum required version.
Console.WriteLine(Environment.OSVersion.Version.CompareTo(OsMinVersion));
```

アプリケーションマニフェストでサポートされているオペレーティングシステムとして表示されていない場合、アプリケーションが Windows 10 を正常に検出できないことに注意してください。

また、アプリケーションがビルドされた .NET Framework のバージョンを確認することもできます。

```csharp
Console.WriteLine(AppDomain.CurrentDomain.SetupInformation.TargetFrameworkName);
```

## <a name="see-also"></a>関連項目

- [構成要素の追加 Windows フォーム](../configure-apps/file-schema/winforms/windows-forms-add-configuration-element.md)
- [Windows フォームのサイズとスケールを調整する](adjusting-the-size-and-scale-of-windows-forms.md)
