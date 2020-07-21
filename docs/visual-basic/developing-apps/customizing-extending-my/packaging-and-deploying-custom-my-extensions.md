---
title: カスタム My 拡張のパッケージ化と配置
ms.date: 08/14/2018
helpviewer_keywords:
- My namespace [Visual Basic], customizing
- My namespace
- My namespace [Visual Basic], extending
ms.assetid: fd89c54b-0290-4c50-95a3-ff17d4487a21
ms.openlocfilehash: 6d2cc2b01b04b30bd3b1a4371352ded20ea8664b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411754"
---
# <a name="package-and-deploy-custom-my-extensions-visual-basic"></a>カスタム My 拡張をパッケージ化して配置する (Visual Basic)

Visual Basic では、Visual Studio テンプレートを使用してカスタムの `My` 名前空間拡張を簡単に配置できます。 `My` 拡張が新しいプロジェクト タイプに不可欠な要素であるプロジェクト テンプレートを作成する場合、テンプレートをエクスポートするときに、カスタムの `My` 拡張コードをプロジェクトに含めることができます。 プロジェクト テンプレートのエクスポートの詳細については、「[方法: プロジェクト テンプレートを作成する](/visualstudio/ide/how-to-create-project-templates)」を参照してください。

カスタムの `My` 拡張が単一のコード ファイルに含まれている場合、そのファイルを、ユーザーが任意の種類の Visual Basic プロジェクトに追加できる項目テンプレートとしてエクスポートできます。 その後、項目テンプレートをカスタマイズして、Visual Basic プロジェクト内のカスタムの `My` の追加機能や動作を有効にすることができます。 これらの機能としては、次のものがあります。

- ユーザーが、Visual Basic プロジェクト デザイナーの **[My 拡張]** ページからカスタムの `My` 拡張を管理できるようにします。

- 指定されたアセンブリへの参照をプロジェクトに追加するときに、カスタムの `My` 拡張が自動的に追加されます。

- **[項目の追加]** ダイアログ ボックスで `My` 拡張の項目テンプレートを非表示にして、プロジェクト項目の一覧に含まれないようにします。

このトピックでは、カスタムの `My` 拡張を非表示の項目テンプレートとしてパッケージ化し、Visual Basic プロジェクト デザイナーの **[My 拡張]** ページから管理できるようにする方法について説明します。 指定されたアセンブリへの参照をプロジェクトに追加するときに、カスタムの `My` 拡張も自動的に追加できます。

## <a name="create-a-my-namespace-extension"></a>My 名前空間拡張を作成する

カスタムの `My` 拡張の展開パッケージを作成する場合、最初のステップとして、拡張を単一のコード ファイルとして作成します。 カスタムの `My` 拡張を作成する方法の詳細とガイダンスについては、「[Visual Basic における My 名前空間の拡張](extending-the-my-namespace.md)」を参照してください。

## <a name="export-a-my-namespace-extension-as-an-item-template"></a>My 名前空間拡張を項目テンプレートとしてエクスポートする

`My` 名前空間拡張を含むコード ファイルを作成した後、そのコード ファイルを Visual Studio 項目テンプレートとしてエクスポートできます。 ファイルを Visual Studio 項目テンプレートとしてエクスポートする手順については、「[方法: 項目テンプレートを作成する](/visualstudio/ide/how-to-create-item-templates)」を参照してください。

> [!NOTE]
> `My` 名前空間拡張に、特定のアセンブリに対する依存関係がある場合、項目テンプレートをカスタマイズして、そのアセンブリへの参照が追加されるときに `My` 名前空間拡張が自動的にインストールされるようにすることができます。 そのため、コード ファイルを Visual Studio 項目テンプレートとしてエクスポートするときにそのアセンブリへの参照を除外する必要があります。

## <a name="customize-the-item-template"></a>項目テンプレートをカスタマイズする

項目テンプレートを Visual Basic プロジェクト デザイナーの **[My 拡張]** ページから管理できるようにすることができます。 また、指定されたアセンブリへの参照をプロジェクトに追加するときに、項目テンプレートも自動的に追加されるようにすることもできます。 これらのカスタマイズを有効にするには、CustomData ファイルという名前の新しいファイルをテンプレートに追加し、.vstemplate ファイル内の XML に新しい要素を追加します。

### <a name="add-the-customdata-file"></a>CustomData ファイルを追加する

CustomData ファイルは、ファイル名拡張子が .CustomData のテキスト ファイルで (ファイル名は、テンプレートにとって意味のある任意の値に設定できます)、XML が含まれています。 CustomData ファイル内の XML は、ユーザーが Visual Basic プロジェクト デザイナーの **[My 拡張]** ページを使用するときに `My` 拡張を含めるように Visual Basic に指示します。 必要に応じて、<`AssemblyFullName>` 属性を CustomData ファイルの XML に追加できます。 これは、特定のアセンブリへの参照をプロジェクトに追加するときにカスタムの `My` 拡張を自動的にインストールするように Visual Basic に指示します。 任意のテキスト エディターまたは XML エディターを使用して CustomData ファイルを作成し、その後、ファイルを項目テンプレートの圧縮フォルダー (.zip ファイル) に追加できます。

たとえば、次の XML は、Microsoft.VisualBasic.PowerPacks.Vs.dll アセンブリへの参照をプロジェクトに追加するときに、Visual Basic プロジェクトの [My 拡張] フォルダーにテンプレート項目を追加する CustomData ファイルの内容を示します。

```xml
<VBMyExtensionTemplate
    ID="Microsoft.VisualBasic.Samples.MyExtensions.MyPrinterInfo"
    Version="1.0.0.0"
    AssemblyFullName="Microsoft.VisualBasic.PowerPacks.vs"
/>
```

この CustomData ファイルには、次の表に一覧表示する属性を持つ <`VBMyExtensionTemplate>` 要素が含まれています。

|属性|説明|
|---|---|
|`ID`|必須です。 拡張の一意の識別子。 この ID を持つ拡張がプロジェクトに既に追加されている場合、ユーザーに対して、再度追加するように要求されません。|
|`Version`|必須です。 項目テンプレートのバージョン番号。|
|`AssemblyFullName`|任意。 アセンブリ名。 このアセンブリへの参照をプロジェクトに追加する場合、ユーザーに対して、この項目テンプレートから `My` 拡張を追加するように要求されます。|

### <a name="add-the-customdatasignature-element-to-the-vstemplate-file"></a>\<CustomDataSignature> 要素を .vstemplate ファイルに追加する

Visual Studio 項目テンプレートを `My` 名前空間拡張として識別するには、項目テンプレートの .vstemplate ファイルも変更する必要があります。 `<CustomDataSignature>` 要素を `<TemplateData>` に追加する必要があります。 次の例に示すように、`<CustomDataSignature>` 要素には、テキスト `Microsoft.VisualBasic.MyExtension` を含める必要があります。

```xml
<CustomDataSignature>Microsoft.VisualBasic.MyExtension</CustomDataSignature>
```

圧縮フォルダー (.zip ファイル) 内のファイルを直接変更することはできません。 圧縮フォルダーから .vstemplate ファイルをコピーし、それを変更して、圧縮フォルダー内の .vstemplate ファイルを、更新したコピーに置き換える必要があります。

次の例は、`<CustomDataSignature>` 要素が追加された .vstemplate ファイルの内容を示します。

```xml
<VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
  <TemplateData>
    <DefaultName>MyCustomExtensionModule.vb</DefaultName>
    <Name>MyPrinterInfo</Name>
    <Description>Custom My Extensions Item Template</Description>
    <ProjectType>VisualBasic</ProjectType>
    <SortOrder>10</SortOrder>
    <Icon>__TemplateIcon.ico</Icon>
    <CustomDataSignature      >Microsoft.VisualBasic.MyExtension</CustomDataSignature>
  </TemplateData>
  <TemplateContent>
    <References />
    <ProjectItem SubType="Code"
                 TargetFileName="$fileinputname$.vb"
                 ReplaceParameters="true"
     >MyCustomExtensionModule.vb</ProjectItem>
  </TemplateContent>
</VSTemplate>
```

## <a name="install-the-template"></a>テンプレートのインストール

テンプレートをインストールするには、圧縮フォルダー ( *.zip* ファイル) を Visual Basic 項目テンプレート フォルダーにコピーします。 既定では、ユーザー項目テンプレートは、 *%USERPROFILE%\Documents\Visual Studio \<Version\>\Templates\ItemTemplates\Visual Basic* にあります。 または、テンプレートを Visual Studio インストーラー ( *.vsi*) ファイルとして発行することもできます。

## <a name="see-also"></a>関連項目

- [Visual Basic における My 名前空間の拡張](extending-the-my-namespace.md)
- [Visual Basic アプリケーション モデルの拡張](extending-the-visual-basic-application-model.md)
- [My で利用可能なオブジェクトのカスタマイズ](customizing-which-objects-are-available-in-my.md)
- [[マイ拡張] ページ (プロジェクト デザイナー)](/visualstudio/ide/reference/my-extensions-page-project-designer-visual-basic)
