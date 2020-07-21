---
title: '方法: ローカライズ可能アプリケーションでリソースを使用する'
ms.date: 03/30/2017
helpviewer_keywords:
- applications [WPF], localizable
- localizable applications [WPF]
ms.assetid: 08539ad6-7fca-4f34-b82b-ff439e11dfa7
ms.openlocfilehash: 8f516a86036656b98add23d38c588b5c19be4d7a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212476"
---
# <a name="how-to-use-resources-in-localizable-apps"></a>方法: ローカライズ可能なアプリでリソースを使用する

ローカライズとは、ユーザー インターフェイスを異なるカルチャに適合させることを意味します。 そのためには、タイトル、キャプション、リスト ボックス項目などのテキストを翻訳する必要があります。 翻訳しやすいように、翻訳される項目はリソース ファイルにまとめられています。 ローカライズ用のリソース ファイルの作成方法については、「[アプリケーションをローカライズする](how-to-localize-an-application.md)」を参照してください。 開発者は、WPF アプリケーションをローカライズ可能にするために、ローカライズ可能なすべてのリソースをリソース アセンブリに組み込む必要があります。 リソース アセンブリはさまざまな言語にローカライズされ、コードビハインドでリソース管理 API が使用されて読み込まれます。

## <a name="example"></a>例

WPF アプリケーションに必要なファイルの 1 つは、プロジェクト ファイル (.proj) です。 アプリケーションで使用するすべてのリソースをプロジェクト ファイルに含める必要があります。 次の XAML の例がこれを示します。

```xaml
<Resource Include="data\picture1.jpg"/>  
<EmbeddedResource Include="data\stringtable.en-US.restext"/>
```

アプリケーションでリソースを使用するには、<xref:System.Resources.ResourceManager> をインスタンス化し、使用するリソースを読み込みます。 次の C# コードは、この設定方法を示します。

[!code-csharp[LocalizationResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]

## <a name="see-also"></a>関連項目

- [アプリをローカライズする](how-to-localize-an-application.md)
