---
title: '方法: Windows アプリケーションにヘルプを提供する'
ms.date: 03/30/2017
helpviewer_keywords:
- Help [Windows Forms], Windows applications
- HTML Help [Windows Forms], Windows Forms
- Windows applications [Windows Forms], providing Help
- HelpProvider component [Windows Forms]
- forms [Windows Forms], providing Help
ms.assetid: 7c4e5cec-2bd2-4f0b-8d75-c2b88929bd61
ms.openlocfilehash: 405de333ce936a864047e827e60f56a930059e26
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84143629"
---
# <a name="how-to-provide-help-in-a-windows-application"></a>方法: Windows アプリケーションにヘルプを提供する

コンポーネントを使用して、 <xref:System.Windows.Forms.HelpProvider> ヘルプファイル内のヘルプトピックを Windows フォームの特定のコントロールにアタッチすることができます。 ヘルプ ファイルの形式には、HTML または HTMLHelp 1.x 以上を指定できます。

## <a name="provide-help"></a>ヘルプの提供

1. Visual Studio の**ツールボックス**から、 <xref:System.Windows.Forms.HelpProvider> コンポーネントをフォームにドラッグします。

     コンポーネントは、Windows フォーム デザイナーの下部にあるトレイに配置されます。

2. [**プロパティ**] ウィンドウで、 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> プロパティを .chm、col、.htm のいずれかのヘルプファイルに設定します。

3. フォーム上の別のコントロールを選択し、[**プロパティ**] ウィンドウでプロパティを設定し <xref:System.Windows.Forms.HelpProvider.SetHelpKeyword%2A> ます。

     これは、 <xref:System.Windows.Forms.HelpProvider> 適切なヘルプトピックを召喚するために、コンポーネントを使用してヘルプファイルに渡される文字列です。

4. [**プロパティ**] ウィンドウで、 <xref:System.Windows.Forms.HelpProvider.SetHelpNavigator%2A> プロパティを列挙体の値に設定し <xref:System.Windows.Forms.HelpNavigator> ます。

     これにより、**HelpKeyword** プロパティがヘルプ システムに渡される方法が決まります。 設定できるオプションとその説明を次の表に示します。

    |メンバー名|説明|
    |-----------------|-----------------|
    |AssociateIndex|指定したトピックのインデックスを指定した URL で実行するように指定します。|
    |Find|指定した URL の検索ページを表示するように指定します。|
    |インデックス|指定した URL のインデックスを表示するように指定します。|
    |KeywordIndex|検索するキーワードと、指定した URL で実行するアクションを指定します。|
    |TableOfContents|HTML 1.0 ヘルプ ファイルの目次を表示するように指定します。|
    |トピック|指定した URL によって参照されるトピックを表示するように指定します。|

 実行時に、 **HelpKeyword**プロパティと**HelpNavigator**プロパティを設定したコントロールにフォーカスがあるときに F1 キーを押すと、そのコンポーネントに関連付けられているヘルプファイルが開きます <xref:System.Windows.Forms.HelpProvider> 。

 現在、**HelpNamespace** プロパティは HTMLHelp 1.x、HTMLHelp 2.0、および HTML の 3 つの形式のヘルプ ファイルをサポートしています。 したがって、 **Helpnamespace**プロパティを Web ページなどのアドレスに設定でき `http://` ます。 プロパティに http:// アドレスを設定すると、既定のブラウザーが開き、**HelpKeyword** プロパティに指定した文字列をアンカーとして使用して Web ページが表示されます。 アンカーは HTML ページの特定の部分にジャンプするために使用されます。

> [!IMPORTANT]
> クライアントから送信された情報は、アプリケーションで使用する前に必ずチェックしてください。 悪意のあるユーザーが、実行可能スクリプトや SQL ステートメントなどのコードの送信 (挿入) を試みる場合があります。 ユーザーからの入力を表示したり、データベースに格納したり、操作したりする前に、安全でない可能性のある情報が含まれていないかどうかを確認してください。 一般的な確認方法としては、ユーザーから入力を受け取ったときに、正規表現を使用して、"SCRIPT" などのキーワードを検索します。

<xref:System.Windows.Forms.HelpProvider>Windows フォームのコントロールのヘルプファイルを表示するように構成している場合でも、コンポーネントを使用してポップアップヘルプを表示することもできます。 詳細については、「[方法: ポップアップ ヘルプを表示する](how-to-display-pop-up-help.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: ポップアップ ヘルプを表示する](how-to-display-pop-up-help.md)
- [ツールヒントを使用したコントロールのヘルプ](control-help-using-tooltips.md)
- [Windows フォームでのヘルプの統合](integrating-user-help-in-windows-forms.md)
- [Windows フォーム](../index.md)
