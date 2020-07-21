---
title: アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル
description: Windows Presentation Foundation (WPF) でのアプリケーション データ ファイルの構成、識別、および使用に関する特別なサポートについて説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF application [WPF], files
- loose resources [WPF]
- content files [WPF]
- Site of Origin files [WPF]
- resource files [WPF]
- remote files [WPF]
- embedded resources [WPF]
- files [WPF]
- referencing application files [WPF]
- application development [WPF], files
- application management [WPF]
ms.assetid: 7ad2943b-3961-41d3-8fc6-1582d43f5d99
ms.openlocfilehash: 324b3eb922f0fd1d1d9ad00105a06a7fbdb8effd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622862"
---
# <a name="wpf-application-resource-content-and-data-files"></a>WPF アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル
Microsoft Windows アプリケーションは、多くの場面で、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]、イメージ、ビデオ、オーディオなどの実行可能ではないデータを格納したファイルを必要とします。 Windows Presentation Foundation (WPF) には、アプリケーション データ ファイルと呼ばれるこれらの種類のデータ ファイルを構成、識別、および使用するための特殊なサポート機能があります。 このサポートの中心となるのは、次のような特定のアプリケーション データ ファイルの種類のセットです。  
  
- **リソース ファイル**:実行可能ファイルまたはライブラリ WPF アセンブリにコンパイルされるデータ ファイル。  
  
- **コンテンツ ファイル**:実行可能 WPF アセンブリとの明示的な関連付けを持つスタンドアロン データ ファイル。  
  
- **起点サイト ファイル**:実行可能 WPF アセンブリとの関連付けを持たないスタンドアロン データ ファイル。  
  
 これらの 3 種類のファイルの重要な違いは、リソース ファイルとコンテンツ ファイルはビルド時に認識されるという点です。アセンブリは、これらを明確に認識します。 ただし、起点サイト ファイルについては、アセンブリはまったく認識しないか、パックの Uniform Resource Identifier (URI) 参照を通じて暗黙的に認識します。後者の場合、参照される起点サイト ファイルが実際に存在することは保証されません。  
  
 アプリケーション データ ファイルを参照するために、Windows Presentation Foundation (WPF) はパッケージの Uniform Resource Identifier (URI) スキームを使用します。このスキームについては、「[WPF におけるパッケージの URI](pack-uris-in-wpf.md)」で詳しく説明します。  
  
 このトピックでは、アプリケーション データ ファイルを構成および使用する方法について説明します。  

<a name="Resource_Files"></a>
## <a name="resource-files"></a>リソース ファイル (Visual Studio)  
 アプリケーション データ ファイルを常にアプリケーションで使用可能にするには、コンパイルしてアプリケーションのメイン実行可能アセンブリまたはその参照アセンブリの 1 つに組み込む必要があります。 この種類のアプリケーション データ ファイルを、"*リソース ファイル*" と呼びます。  
  
 リソース ファイルは、次のときに使用します。  
  
- コンパイルしてアセンブリに組み込んだ後に、リソース ファイルのコンテンツを更新する必要がない。  
  
- ファイルの依存関係の数を減らして、アプリケーション配布の複雑さを軽減する必要がある。  
  
- アプリケーション データ ファイルをローカライズ可能にする必要がある (「[WPF のグローバリゼーションおよびローカリゼーションの概要](../advanced/wpf-globalization-and-localization-overview.md)」を参照)。  
  
> [!NOTE]
> このセクションで説明するリソース ファイルは、「[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)」で説明されているリソース ファイルとも、「[アプリケーション リソースの管理 (.NET)](/visualstudio/ide/managing-application-resources-dotnet)」で説明されている埋め込みリソースまたはリンクされたリソースとも異なります。  
  
### <a name="configuring-resource-files"></a>リソース ファイルの構成  
 WPF では、リソース ファイルとは Microsoft Build Engine (MSBuild) プロジェクトに `Resource` 項目としてインクルードされるファイルです。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Resource Include="ResourceFile.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> Visual Studio では、リソース ファイルを作成するにはファイルをプロジェクトに追加し、その `Build Action` を `Resource` に設定します。  
  
 プロジェクトをビルドするときに、MSBuild によってリソースがコンパイルされ、アセンブリに組み込まれます。  
  
### <a name="using-resource-files"></a>リソース ファイルの使用  
 リソース ファイルを読み込むには、<xref:System.Windows.Application> クラスの <xref:System.Windows.Application.GetResourceStream%2A> メソッドを呼び出し、目的のリソース ファイルを識別するパック URI を渡します。 <xref:System.Windows.Application.GetResourceStream%2A> からは、<xref:System.Windows.Resources.StreamResourceInfo> オブジェクトが返されます。このオブジェクトによってリソース ファイルが <xref:System.IO.Stream> として公開され、そのコンテンツ タイプが記述されます。  
  
 次に示すコードの例では、<xref:System.Windows.Application.GetResourceStream%2A> を使用して <xref:System.Windows.Controls.Page> リソース ファイルを読み込み、<xref:System.Windows.Controls.Frame> (`pageFrame`) のコンテンツとして設定する方法を示します。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadapageresourcefilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadapageresourcefilemanuallycode)]  
  
 <xref:System.Windows.Application.GetResourceStream%2A> を呼び出すと <xref:System.IO.Stream> にアクセスできますが、設定に使用するプロパティの型にそれを変換する追加作業を実行する必要があります。 代わりに、WPF を使用して、コードでリソース ファイルをある型のプロパティに直接読み込むことによって <xref:System.IO.Stream> を開いたり変換したりできます。  
  
 次の例は、コードを使用して <xref:System.Windows.Controls.Page> を直接 <xref:System.Windows.Controls.Frame> (`pageFrame`) に読み込む方法を示しています。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadpageresourcefilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadpageresourcefilefromcode)]  
  
 次の例は、上の例と同じ意味のマークアップです。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml#loadpageresourcefilefromxaml)]  
  
### <a name="application-code-files-as-resource-files"></a>リソース ファイルとしてのアプリケーション コード ファイル  
 ウィンドウ、ページ、フロー ドキュメント、リソース ディクショナリなどのパック URI を使用して、特殊な WPF アプリケーション コード ファイルのセットを参照できます。 たとえば、ウィンドウまたはページを参照するパック URI を使用して <xref:System.Windows.Application.StartupUri%2A?displayProperty=nameWithType> プロパティを設定すると、アプリケーションの開始時にそのウィンドウまたはページを読み込むことができます。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#SetApplicationStartupURI](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/App.xaml#setapplicationstartupuri)]  
  
 これを実行できるのは、次に示すように XAML ファイルが MSBuild プロジェクトに `Page` 項目としてインクルードされている場合です。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Page Include="MainWindow.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> Visual Studio では、新しい <xref:System.Windows.Window>、<xref:System.Windows.Navigation.NavigationWindow>、<xref:System.Windows.Controls.Page>、<xref:System.Windows.Documents.FlowDocument>、または <xref:System.Windows.ResourceDictionary> をプロジェクトに追加したときの、マークアップ ファイルの `Build Action` の既定値は `Page` です。  
  
 `Page` 項目を持つプロジェクトがコンパイルされるときに、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 項目はバイナリ形式に変換され、コンパイルされて関連するアセンブリに組み込まれます。 したがって、これらのファイルは、通常のリソース ファイルと同様に使用できます。  
  
> [!NOTE]
> `Resource` 項目として構成されている [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルに分離コード ファイルがない場合は、元の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] をバイナリに変換したものではなく、元の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] がコンパイルされてアセンブリに組み込まれます。  
  
<a name="Content_Files"></a>
## <a name="content-files"></a>コンテンツ ファイル  
 *コンテンツ ファイル*は、実行可能アセンブリと共に圧縮しないファイルとして配布されます。 コンテンツ ファイルはコンパイルされてアセンブリに組み込まれるのではありませんが、アセンブリのコンパイル時に、各コンテンツ ファイルとの関連付けを確立するメタデータが使用されます。  
  
 アプリケーションに必要な特定のアプリケーション データ ファイルのセットが更新されても、そのファイルを使用するアセンブリを再コンパイルせずに、コンテンツ ファイルを使用する必要があります。  
  
### <a name="configuring-content-files"></a>コンテンツ ファイルの構成  
 コンテンツ ファイルをプロジェクトに追加するには、アプリケーション データ ファイルを `Content` 項目としてインクルードする必要があります。 さらに、コンテンツ ファイルはコンパイルされて直接アセンブリに組み込まれるものではないため、ビルド アセンブリからの相対的な場所にコンテンツ ファイルがコピーされることを指定するために MSBuild `CopyToOutputDirectory` メタデータ要素を設定する必要があります。 プロジェクトがビルドされるたびにビルド出力フォルダーにリソースをコピーする場合は、`CopyToOutputDirectory` メタデータ要素の設定値を `Always` とします。 それ以外の場合は、リソースの最新バージョンだけがビルド出力フォルダーにコピーされるように、`PreserveNewest` 値を使用して設定します。  
  
 次に示すファイルは、新しいバージョンのリソースがプロジェクトに追加された場合にのみビルド出力フォルダーにコピーされるコンテンツ ファイルとして構成されています。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Content Include="ContentFile.xaml">  
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
    </Content>  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> Visual Studio では、コンテンツ ファイルを作成するにはファイルをプロジェクトに追加し、その `Build Action` を `Content` に設定します。また、`Copy to Output Directory` を `Copy always` (`Always` と同じ) および `Copy if newer` (`PreserveNewest` と同じ) に設定します。  
  
 プロジェクトがビルドされるときに、<xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 属性はコンパイルされて各コンテンツ ファイルのアセンブリのメタデータとなります。  
  
 `[assembly: AssemblyAssociatedContentFile("ContentFile.xaml")]`  
  
 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 値の意味は、プロジェクト内のコンテンツ ファイルの位置を表す相対パスです。 たとえば、コンテンツ ファイルがプロジェクト サブフォルダー内にある場合は、追加のパス情報が <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 値に組み込まれます。  
  
 `[assembly: AssemblyAssociatedContentFile("Resources/ContentFile.xaml")]`  
  
 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 値は、ビルド出力フォルダー内のコンテンツ ファイルへのパスの値でもあります。  
  
### <a name="using-content-files"></a>コンテンツ ファイルの使用  
 コンテンツ ファイルを読み込むには、<xref:System.Windows.Application> クラスの <xref:System.Windows.Application.GetContentStream%2A> メソッドを呼び出し、目的のコンテンツ ファイルを識別するパック URI を渡します。 <xref:System.Windows.Application.GetContentStream%2A> からは、<xref:System.Windows.Resources.StreamResourceInfo> オブジェクトが返されます。このオブジェクトによってコンテンツ ファイルが <xref:System.IO.Stream> として公開され、そのコンテンツ タイプが記述されます。  
  
 次に示すコードの例では、<xref:System.Windows.Application.GetContentStream%2A> を使用して <xref:System.Windows.Controls.Page> コンテンツ ファイルを読み込み、<xref:System.Windows.Controls.Frame> (`pageFrame`) のコンテンツとして設定する方法を示します。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadapagecontentfilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadapagecontentfilemanuallycode)]  
  
 <xref:System.Windows.Application.GetContentStream%2A> を呼び出すと <xref:System.IO.Stream> にアクセスできますが、設定に使用するプロパティの型にそれを変換する追加作業を実行する必要があります。 代わりに、WPF を使用して、コードでリソース ファイルをある型のプロパティに直接読み込むことによって <xref:System.IO.Stream> を開いたり変換したりできます。  
  
 次の例は、コードを使用して <xref:System.Windows.Controls.Page> を直接 <xref:System.Windows.Controls.Frame> (`pageFrame`) に読み込む方法を示しています。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadpagecontentfilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadpagecontentfilefromcode)]  
  
 次の例は、上の例と同じ意味のマークアップです。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageContentFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml#loadpagecontentfilefromxaml)]  
  
<a name="Site_of_Origin_Files"></a>
## <a name="site-of-origin-files"></a>起点サイト ファイル  
 リソース ファイルは、共に配布されるアセンブリとの間に明示的な関係を持っており、この関係は <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> で定義されます。 ただし、アセンブリとアプリケーション データ ファイル間に暗黙的な関係を持たせる、または関係を持たせない場合があります。たとえば次のような場合です。  
  
- コンパイル時にファイルが存在しない場合。  
  
- アセンブリが必要とするファイルが、実行時までわからない場合。  
  
- 関連付けられているアセンブリを再コンパイルせずにファイルを更新可能にする場合。  
  
- オーディオやビデオなど大容量のデータ ファイルを使用するアプリケーションで、ユーザーが選択した場合にのみファイルをダウンロードする場合。  
  
 このような種類のファイルを、`file:///` スキームや `http://` スキームなど、従来の URI スキームを使用して読み込むこともできます。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#AbsolutePackUriFileHttpReferenceXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/AbsolutePackUriPage.xaml#absolutepackurifilehttpreferencexaml)]  
  
 ただし、`file:///` スキームや `http://` スキームを使用する場合は、アプリケーションに完全信頼が必要です。 アプリケーションが、インターネットまたはイントラネットから起動された XAML ブラウザー アプリケーション (XBAP) であり、その場所から起動されたアプリケーションに対して許可されるアクセス許可のセットのみがアプリケーションによって要求される場合は、アプリケーションの起点サイト (起動場所) からのみ圧縮しないファイルを読み込むことができます。 このようなファイルを、"*起点サイト*" ファイルと呼びます。  
  
 起点サイト ファイルは部分信頼アプリケーションの唯一のオプションですが、部分信頼アプリケーション以外でも使用できます。 完全信頼アプリケーションでも、読み込むアプリケーション データ ファイルがビルド時点では不明な場合があります。完全信頼アプリケーションでは file:/// を使用できますが、アプリケーション データ ファイルがアプリケーション アセンブリと同じフォルダーにインストールされることも、サブフォルダーにインストールされることも考えられます。 この場合は、起点サイト参照を使用する方が、file:/// を使用するよりも簡単です。file:/// を使用するには、ファイルの完全パスを指定する必要があるためです。  
  
> [!NOTE]
> 起点サイト ファイルは、コンテンツ ファイルとは異なり、クライアント コンピューター上の XAML ブラウザー アプリケーション (XBAP) でキャッシュされません。 したがって、起点サイト ファイルは明確に要求されたときにのみダウンロードされます。 XAML ブラウザー アプリケーション (XBAP) アプリケーションで使用する大容量のメディア ファイルを起点サイト ファイルとして構成すると、アプリケーションの最初の起動時間が大幅に短縮され、ファイルは要求されたときにのみダウンロードされるようになります。  
  
### <a name="configuring-site-of-origin-files"></a>起点サイト ファイルの構成  
 起点サイト ファイルがコンパイル時に存在しない場合や不明な場合は、従来の配置機構 (`XCopy` コマンドライン プログラムまたは Microsoft Windows インストーラーなど) を使用して、必要なファイルが実行時には使用可能になっていることを確認する必要があります。  
  
 起点サイトに配置されるファイルがコンパイル時にわかっている場合でも、明示的な依存関係を持たせないためには、そのファイルを MSBuild プロジェクトに `None` 項目として追加します。 コンテンツ ファイルと同様に、MSBuild `CopyToOutputDirectory` 属性を設定して、ビルド アセンブリからの相対位置に起点サイト ファイルがコピーされることを指定する必要があります。値には、`Always` または `PreserveNewest` を指定します。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <None Include="PageSiteOfOriginFile.xaml">  
    <CopyToOutputDirectory>Always</CopyToOutputDirectory>  
  </None>  
  ...  
</Project>  
```  
  
> [!NOTE]
> Visual Studio では、起点サイト ファイルを作成するにはファイルをプロジェクトに追加し、その `Build Action` を `None` に設定します。  
  
 プロジェクトをビルドするときに、指定したファイルが MSBuild によってビルド出力フォルダーにコピーされます。  
  
### <a name="using-site-of-origin-files"></a>起点サイト ファイルの使用  
 起点サイト ファイルを読み込むには、<xref:System.Windows.Application> クラスの <xref:System.Windows.Application.GetRemoteStream%2A> メソッドを呼び出し、目的の起点サイト ファイルを識別するパック URI を渡します。 <xref:System.Windows.Application.GetRemoteStream%2A> からは、<xref:System.Windows.Resources.StreamResourceInfo> オブジェクトが返されます。このオブジェクトによって起点サイト ファイルが <xref:System.IO.Stream> として公開され、そのコンテンツ タイプが記述されます。  
  
 次に示すコードの例では、<xref:System.Windows.Application.GetRemoteStream%2A> を使用して <xref:System.Windows.Controls.Page> 起点サイト ファイルを読み込み、<xref:System.Windows.Controls.Frame> (`pageFrame`) のコンテンツとして設定する方法を示します。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadapagesoofilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadapagesoofilemanuallycode)]  
  
 <xref:System.Windows.Application.GetRemoteStream%2A> を呼び出すと <xref:System.IO.Stream> にアクセスできますが、設定に使用するプロパティの型にそれを変換する追加作業を実行する必要があります。 代わりに、WPF を使用して、コードでリソース ファイルをある型のプロパティに直接読み込むことによって <xref:System.IO.Stream> を開いたり変換したりできます。  
  
 次の例は、コードを使用して <xref:System.Windows.Controls.Page> を直接 <xref:System.Windows.Controls.Frame> (`pageFrame`) に読み込む方法を示しています。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadpagesoofilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadpagesoofilefromcode)]  
  
 次の例は、上の例と同じ意味のマークアップです。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml#loadpagesoofilefromxaml)]  
  
<a name="Rebuilding_after_Changing_Build_Type"></a>
## <a name="rebuilding-after-changing-build-type"></a>ビルドの種類を変更した後のリビルド  
 アプリケーション データ ファイルのビルドの種類を変更した後は、変更を確実に反映するためにアプリケーション全体をリビルドする必要があります。 アプリケーションのみをビルドしても、変更は適用されません。  
  
## <a name="see-also"></a>関連項目

- [WPF におけるパッケージの URI](pack-uris-in-wpf.md)
