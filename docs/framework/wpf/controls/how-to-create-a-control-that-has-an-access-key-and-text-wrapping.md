---
title: '方法: アクセス キーおよびテキスト折り返し機能を持つコントロールを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- access keys [WPF], control for
- controls [WPF], text wrapping
- wrapping text [WPF]
- keys [WPF], control for
- controls [WPF], access keys
- text wrapping [WPF]
ms.assetid: 205099d9-2551-4302-a25e-a15af9f67e04
ms.openlocfilehash: 48e439719afa2426b5d8f822c621080cdc32514e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910924"
---
# <a name="how-to-create-a-control-that-has-an-access-key-and-text-wrapping"></a>方法: アクセス キーおよびテキスト折り返し機能を持つコントロールを作成する
この例では、アクセス キーがありテキスト折り返しをサポートするコントロールを作成する方法を説明します。 この例では、<xref:System.Windows.Controls.Label> を使用してこれらの概念を図解します。  
  
## <a name="example"></a>例  
 **ラベルにテキスト折り返し機能を追加する**  
  
 <xref:System.Windows.Controls.Label> コントロールはテキストの折り返しに対応していません。 複数の行を折り返せるラベルが必要な場合には、テキスト折り返し機能をサポートしている別の要素を入れ子にすることができます。 次の例では、<xref:System.Windows.Controls.TextBlock> を使用して複数行のテキストを折り返せるラベルを作成する方法を説明します。  
  
 [!code-xaml[LabelSnippet#5](~/samples/snippets/csharp/VS_Snippets_Wpf/LabelSnippet/CS/Pane1.xaml#5)]  
  
 **アクセス キーおよびテキスト折り返し機能をラベルに追加する**  
  
 アクセスキー (ニーモニック) のある <xref:System.Windows.Controls.Label> が必要な場合、<xref:System.Windows.Controls.Label> 内にある <xref:System.Windows.Controls.AccessText> 要素を使用します。  
  
 <xref:System.Windows.Controls.Label>、<xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.RadioButton>、<xref:System.Windows.Controls.CheckBox>、<xref:System.Windows.Controls.MenuItem>、<xref:System.Windows.Controls.TabItem>、<xref:System.Windows.Controls.Expander>、<xref:System.Windows.Controls.GroupBox> などのコントロールには、既定のコントロール テンプレートがあります。 これらのテンプレートには <xref:System.Windows.Controls.ContentPresenter> が含まれています。 <xref:System.Windows.Controls.ContentPresenter> で設定できるプロパティの 1 つに <xref:System.Windows.Controls.ContentPresenter.RecognizesAccessKey%2A>="true" があります。これを利用し、コントロールのアクセス キーを指定できます。  
  
 次の例では、アクセス キーがあり、テキスト折り返しをサポートする <xref:System.Windows.Controls.Label> を作成する方法を説明します。 この例ではテキスト折り返し機能を有効にするために、<xref:System.Windows.Controls.AccessText.TextWrapping%2A> プロパティを設定し、下線文字を使用してアクセス キーを指定します。 (下線文字の直後の文字はアクセス キーになります。)  
  
 [!code-xaml[LabelSnippet#4](~/samples/snippets/csharp/VS_Snippets_Wpf/LabelSnippet/CS/Pane1.xaml#4)]  
  
## <a name="see-also"></a>関連項目

- [方法: ラベルのターゲット プロパティを設定する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752101(v=vs.90))
