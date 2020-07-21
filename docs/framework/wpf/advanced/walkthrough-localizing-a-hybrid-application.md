---
title: 'チュートリアル: ハイブリッド アプリケーションのローカライズ'
ms.date: 08/18/2018
helpviewer_keywords:
- localization [WPF interoperability]
- hybrid applications [WPF interoperability]
ms.assetid: fbc0c54e-930a-4c13-8e9c-27b83665010a
ms.openlocfilehash: 69aa5ae145ffe378b7a4547e5a33826965bf7894
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111115"
---
# <a name="walkthrough-localizing-a-hybrid-application"></a>チュートリアル: ハイブリッド アプリケーションのローカライズ

このチュートリアルでは、Windows フォーム ベースのハイブリッド アプリケーションで [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の要素をローカライズする方法について説明します。

このチュートリアルでは、以下のタスクを行います。

- Windows フォーム ホスト プロジェクトの作成。

- ローカライズ可能なコンテンツの追加。

- ローカライズの有効化。

- リソース識別子の割り当て。

- LocBaml ツールを使用したサテライト アセンブリの生成。

このチュートリアルで説明するタスクの完全なコード リストについては、[ハイブリッド アプリケーションのローカライズのサンプル](https://go.microsoft.com/fwlink/?LinkID=160015)を参照してください。

完了すると、ローカライズされたハイブリッド アプリケーションが完成します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio 2017

## <a name="creating-the-windows-forms-host-project"></a>Windows フォーム ホスト プロジェクトの作成

最初のステップでは、Windows フォーム アプリケーション プロジェクトを作成し、ローカライズするコンテンツが含まれる [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 要素を追加します。

### <a name="to-create-the-host-project"></a>ホスト プロジェクトを作成するには

1. `LocalizingWpfInWf` という名前の **WPF アプリ** プロジェクトを作成します。  ( **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]**  >  **[Visual C#]** または **[Visual Basic]**  >  **[クラシック デスクトップ]**  >  **[WPF アプリケーション]** )。

2. `SimpleControl` という名前の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> 要素をプロジェクトに追加します。

3. <xref:System.Windows.Forms.Integration.ElementHost> コントロールを使用して、フォームに `SimpleControl` 要素を配置します。 詳細については、「[チュートリアル:Windows フォームでの 3D WPF 複合コントロールのホスト](walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md)」を参照してください。

## <a name="adding-localizable-content"></a>ローカライズ可能なコンテンツの追加

次に、Windows フォームのラベル コントロールを追加し、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 要素のコンテンツにローカライズ可能な文字列を設定します。

### <a name="to-add-localizable-content"></a>ローカライズ可能なコンテンツを追加するには

1. **ソリューション エクスプローラー**で、**SimpleControl.xaml** をダブルクリックして WPF デザイナーで開きます。

2. 次のコードを使用して、<xref:System.Windows.Controls.Button> コントロールのコンテンツを設定します。

     [!code-xaml[LocalizingWpfInWf#10](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl0.xaml#10)]

3. **ソリューション エクスプローラー**で、**Form1** をダブルクリックして Windows フォーム デザイナーで開きます。

4. **[ツールボックス]** を開き、 **[Label]** をダブルクリックして、フォームにラベル コントロールを追加します。 <xref:System.Windows.Forms.Control.Text%2A> プロパティの値を `"Hello"` に設定します。

5. **F5** キーを押してアプリケーションをビルドし、実行します。

     `SimpleControl` 要素とラベル コントロールの両方に、 **"Hello"** というテキストが表示されます。

## <a name="enabling-localization"></a>ローカライズの有効化

Windows フォーム デザイナーには、サテライト アセンブリでローカライズを有効にするための設定が用意されています。

### <a name="to-enable-localization"></a>ローカライズを有効にするには

1. **ソリューション エクスプローラー**で、**Form1.cs** をダブルクリックして Windows フォーム デザイナーで開きます。

2. **[プロパティ]** ウィンドウで、フォームの **Localizable** プロパティの値を `true` に設定します。

3. **[プロパティ]** ウィンドウで、 **[Language]** プロパティの値を **[スペイン語 (スペイン)]** に設定します。

4. Windows フォーム デザイナーでラベル コントロールを選択します。

5. **[プロパティ]** ウィンドウで、<xref:System.Windows.Forms.Control.Text%2A> プロパティの値を `"Hola"` に設定します。

     Form1.es-ES.resx という名前の新しいリソース ファイルがプロジェクトに追加されます。

6. **ソリューション エクスプローラー**で、**Form1.cs** を右クリックし、 **[コードの表示]** をクリックしてコード エディターで開きます。

7. `Form1` コンストラクターで `InitializeComponent` を呼び出している場所の前に、次のコードをコピーします。

     [!code-csharp[LocalizingWpfInWf#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/Form1.cs#2)]

8. **ソリューション エクスプローラー**で、**LocalizingWpfInWf** を右クリックして **[プロジェクトのアンロード]** をクリックします。

     プロジェクト名に、 **[(使用不可)]** というラベルが付けられます。

9. **LocalizingWpfInWf** を右クリックして、 **[LocalizingWpfInWf.csproj の編集]** をクリックします。

     コード エディターでプロジェクト ファイルが開かれます。

10. 次の行を、プロジェクト ファイルの最初の `PropertyGroup` にコピーします。

    ```xml
    <UICulture>en-US</UICulture>
    ```

11. プロジェクト ファイルを保存して閉じます。

12. **ソリューション エクスプローラー**で、**LocalizingWpfInWf** を右クリックして **[プロジェクトの再読み込み]** をクリックします。

## <a name="assigning-resource-identifiers"></a>リソース識別子の割り当て

リソース識別子を使用して、ローカライズ可能なコンテンツをリソース アセンブリにマップできます。 `updateuid` オプションを指定すると、MsBuild.exe アプリケーションによってリソース識別子が自動的に割り当てられます。

### <a name="to-assign-resource-identifiers"></a>リソース識別子を割り当てるには

1. [スタート] メニューから、開発者コマンド プロンプト for Visual Studio を開きます。

2. 次のコマンドを使用して、ローカライズ可能なコンテンツにリソース識別子を割り当てます。

    ```console
    msbuild -t:updateuid LocalizingWpfInWf.csproj
    ```

3. **ソリューション エクスプローラー**で、**SimpleControl.xaml** をダブルクリックしてコード エディターで開きます。 `msbuild` コマンドによって、`Uid` 属性がすべての要素に追加されていることがわかります。 これにより、リソース識別子の割り当てによるローカライズが容易になります。

     [!code-xaml[LocalizingWpfInWf#20](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl.xaml#20)]

4. **F6** キーを押してソリューションをビルドします。

## <a name="using-locbaml-to-produce-a-satellite-assembly"></a>LocBaml を使用したサテライト アセンブリの生成

ローカライズされたコンテンツは、リソース専用の "*サテライト アセンブリ*" に格納されます。 LocBaml.exe コマンドライン ツールを使用して、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コンテンツに対するローカライズされたアセンブリを生成します。

### <a name="to-produce-a-satellite-assembly"></a>サテライト アセンブリを生成するには

1. LocBaml.exe をプロジェクトの obj\Debug フォルダーにコピーします。 詳細については、「[アプリケーションをローカライズする](how-to-localize-an-application.md)」を参照してください。

2. コマンド プロンプト ウィンドウで、次のコマンドを使用してリソース文字列を一時ファイルに抽出します。

    ```console
    LocBaml /parse LocalizingWpfInWf.g.en-US.resources /out:temp.csv
    ```

3. Visual Studio または他のテキスト エディターを使用して、temp.csv ファイルを開きます。 文字列 `"Hello"` を、スペイン語の翻訳 `"Hola"` に置き換えます。

4. temp.csv ファイルを保存します。

5. 次のコマンドを使用して、ローカライズされたリソース ファイルを生成します。

    ```console
    LocBaml /generate /trans:temp.csv LocalizingWpfInWf.g.en-US.resources /out:. /cul:es-ES
    ```

     LocalizingWpfInWf.g.es-ES.resources ファイルが obj\Debug フォルダーに作成されます。

6. 次のコマンドを使用して、ローカライズされたサテライト アセンブリをビルドします。

    ```console
    Al.exe /out:LocalizingWpfInWf.resources.dll /culture:es-ES /embed:LocalizingWpfInWf.Form1.es-ES.resources /embed:LocalizingWpfInWf.g.es-ES.resources
    ```

     LocalizingWpfInWf.resources.dll ファイルが obj\Debug フォルダーに作成されます。

7. LocalizingWpfInWf.resources.dll ファイルをプロジェクトの bin\Debug\es-ES フォルダーにコピーします。 既存のファイルを置き換えます。

8. プロジェクトの bin\Debug フォルダーにある LocalizingWpfInWf.exe を実行します。 アプリケーションをリビルドしないでください。リビルドすると、サテライト アセンブリが上書きされます。

     アプリケーションで、英語の文字列ではなく、ローカライズされた文字列が表示されます。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [アプリケーションをローカライズする](how-to-localize-an-application.md)
- [チュートリアル: Windows フォームのローカリゼーション](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/y99d1cd3(v=vs.100))
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
