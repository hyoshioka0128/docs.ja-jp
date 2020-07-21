---
title: '方法: Windows サービスをインストールおよびアンインストールする'
ms.date: 02/05/2019
helpviewer_keywords:
- Windows Service applications, deploying
- services, uninstalling
- services, installing
- installing Windows Services
- uninstalling applications, apps, Windows services
- installation, Windows services
- uninstalling Windows services
- installutil.exe tool
ms.assetid: c89c5169-f567-4305-9d62-db31a1de5481
author: ghogen
ms.openlocfilehash: 259b353edc269a77a51e790544018481a53af188
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596359"
---
# <a name="how-to-install-and-uninstall-windows-services"></a>方法: Windows サービスをインストールおよびアンインストールする

.NET Framework を使用して Windows サービスを開発している場合は、[*InstallUtil.exe*](../tools/installutil-exe-installer-tool.md) コマンド ライン ユーティリティまたは [PowerShell](/powershell/scripting/overview) を使用してサービス アプリをすばやくインストールできます。 ユーザーがインストールおよびアンインストールできる Windows サービスをリリースする開発者は、InstallShield を使用する必要があります。 詳細については、「[インストーラー パッケージを作成する (Windows デスクトップ)](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop)」を参照してください。

> [!WARNING]
> サービスをコンピューターからアンインストールする場合は、この記事の手順には従わないでください。 代わりに、サービスをインストールしたプログラムまたはソフトウェア パッケージを確認し、[設定] で **[アプリ]** を選択してそのプログラムをアンインストールします。 多くのサービスが Windows の不可欠な構成要素であることに注意してください。それらを削除すると、システムが不安定になることがあります。

この記事の手順を使用するには、まず、Windows サービスにサービス インストーラーを追加する必要があります。 詳細については、「[チュートリアル:Windows サービス アプリケーションを作成する](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)」を参照してください。

Windows サービス プロジェクトを、F5 キーを押して Visual Studio 開発環境から直接実行することはできません。 プロジェクトを実行するには、プロジェクトにサービスを事前にインストールする必要があります。

> [!TIP]
> **サーバー エクスプローラー**を使用して、サービスがインストールまたはアンインストールされているかどうかを確認できます。 詳細については、[Visual Studio でのサーバー エクスプローラーの使用方法](https://support.microsoft.com/help/316649/how-to-use-the-server-explorer-in-visual-studio-net-and-visual-studio)に関するページを参照してください。

### <a name="install-your-service-manually-using-installutilexe-utility"></a>Installutil.exe ユーティリティを使用してサービスを手動でインストールする

1. **[スタート]** メニューから **[Visual Studio \<*version*>]** ディレクトリを選択し、 **[VS 用開発者コマンド プロンプト\<*version*>]** を選択します。

     Visual Studio 用開発者コマンド プロンプトが表示されます。

2. プロジェクトのコンパイル済み実行可能ファイルが格納されているディレクトリに移動します。

3. プロジェクトの実行可能ファイルをパラメーターとして指定し、コマンド プロンプトから *InstallUtil.exe* を実行します。

    ```console
    installutil <yourproject>.exe
    ```

     Visual Studio 用開発者コマンド プロンプトを使用している場合、*InstallUtil.exe* はシステム パス上にあるはずです。 ない場合は、パスに追加するか、完全修飾パスを使用して起動します。 このツールは、.NET Framework と共に *%WINDIR%\Microsoft.NET\Framework[64]\\<フレームワーク_バージョン\>* フォルダーにインストールされます。

     次に例を示します。
     - 32 ビット バージョンの .NET Framework 4 または 4.5 以降では、Windows のインストール ディレクトリが *C:\Windows* の場合、既定のパスは *C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe* です。
     - 64 ビット バージョンの .NET Framework 4 または 4.5 以降では、既定のパスは *C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe* です。

### <a name="uninstall-your-service-manually-using-installutilexe-utility"></a>Installutil.exe ユーティリティを使用してサービスを手動でアンインストールする

1. **[スタート]** メニューから **[Visual Studio \<*version*>]** ディレクトリを選択し、 **[VS 用開発者コマンド プロンプト\<*version*>]** を選択します。

     Visual Studio 用開発者コマンド プロンプトが表示されます。

2. プロジェクトの出力先ファイルをパラメーターとして指定し、コマンド プロンプトから *InstallUtil.exe* を実行します。

    ```console
    installutil /u <yourproject>.exe
    ```

3. 実行可能ファイルを削除した後も、レジストリ内にサービスが存在したままになることがあります。 このような場合は、コマンド [sc delete](/windows-server/administration/windows-commands/sc-delete) を使って、レジストリからサービスのエントリを削除します。

### <a name="install-your-service-manually-using-powershell"></a>PowerShell を使用してサービスを手動でインストールする

1. **スタート** メニューから、**Windows PowerShell** ディレクトリを選択し、 **[Windows PowerShell]** を選択します。

2. プロジェクトのコンパイル済み実行可能ファイルが格納されているディレクトリに移動します。

3. プロジェクトの出力とサービス名をパラメーターとして指定して、[**New-Service**](/powershell/module/microsoft.powershell.management/new-service) コマンドレットを実行します。

    ```powershell
    New-Service -Name "YourServiceName" -BinaryPathName <yourproject>.exe
    ```

### <a name="uninstall-your-service-manually-using-powershell"></a>PowerShell を使用してサービスを手動でアンインストールする

1. **スタート** メニューから、**Windows PowerShell** ディレクトリを選択し、 **[Windows PowerShell]** を選択します。

2. サービスの名前をパラメーターとして指定して、[**Remove-Service**](/powershell/module/microsoft.powershell.management/remove-service) コマンドレットを実行します。

    ```powershell
    Remove-Service -Name "YourServiceName"
    ```

3. 実行可能ファイルを削除した後も、レジストリ内にサービスが存在したままになることがあります。 このような場合は、コマンド [sc delete](/windows-server/administration/windows-commands/sc-delete) を使って、レジストリからサービスのエントリを削除します。

    ```powershell
    sc.exe delete "YourServiceName"
    ```

## <a name="see-also"></a>関連項目

- [Windows サービス アプリケーションの概要](introduction-to-windows-service-applications.md)
- [方法: Windows サービスを作成する](how-to-create-windows-services.md)
- [方法: サービス アプリケーションにインストーラーを追加する](how-to-add-installers-to-your-service-application.md)
- [Installutil.exe (インストーラー ツール)](../tools/installutil-exe-installer-tool.md)
