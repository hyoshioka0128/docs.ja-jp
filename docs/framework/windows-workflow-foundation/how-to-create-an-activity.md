---
title: '方法: アクティビティを作成する'
description: この記事では、Workflow Foundation で2つのアクティビティを作成する方法を示します。1つはコードを使用してロジックを実装し、もう1つは他のアクティビティを使用して定義します。
ms.date: 09/14/2018
dev_langs:
- csharp
- vb
ms.assetid: c09b1e99-21b5-4d96-9c04-ec31db3f4436
ms.openlocfilehash: dae099d102b0c85d09a1ef8bcce56e8a9096bd20
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83419591"
---
# <a name="how-to-create-an-activity"></a>方法: アクティビティを作成する

アクティビティは [!INCLUDE[wf1](../../../includes/wf1-md.md)] の動作の中心的な単位です。 アクティビティの実行ロジックはマネージド コードで実装できます。または他のアクティビティを使用して実装できます。 このトピックでは、2 つのアクティビティを作成する方法について説明します。 最初のアクティビティは、コードを使用してその実行ロジックを実装する単純なアクティビティです。 2 番目のアクティビティの実装は他のアクティビティを使用して定義されています。 これらのアクティビティは、チュートリアルの次の手順で使用します。

> [!NOTE]
> チュートリアルの完成版をダウンロードするには、「 [Windows Workflow Foundation (WF45) - Getting Started Tutorial (Windows Workflow Foundation (WF45) - チュートリアル入門)](https://go.microsoft.com/fwlink/?LinkID=248976)」を参照してください。

## <a name="create-the-activity-library-project"></a>アクティビティライブラリプロジェクトを作成する

1. Visual Studio を開き**New**  >  、[**ファイル**] メニューの [新しい**プロジェクト**] をクリックします。

2. [**新しいプロジェクト**] ダイアログの [**インストール済み**] カテゴリで、[ **Visual C#**  >  **ワークフロー** ] (または**Visual Basic**  >  **ワークフロー**) を選択します。

    > [!NOTE]
    > [**ワークフロー**テンプレート] カテゴリが表示されない場合は、Visual Studio の**Windows Workflow Foundation**コンポーネントのインストールが必要になることがあります。 [**新しいプロジェクト**] ダイアログの左側にある [ **Visual Studio インストーラーを開く**] リンクをクリックします。 Visual Studio インストーラーで、[**個々のコンポーネント**] タブを選択します。次に、[**開発アクティビティ**] カテゴリで、[ **Windows Workflow Foundation** ] コンポーネントを選択します。 [**変更**] を選択してコンポーネントをインストールします。

3. [**アクティビティライブラリ**] プロジェクトテンプレートを選択します。 [**名前**] ボックスに「`NumberGuessWorkflowActivities`」と入力して、[**OK**] をクリックします。

4. **ソリューション エクスプローラー**で、[**Activity1.xaml**] を右クリックし、[**削除**] を選択します。 [**OK**] をクリックして確定します。

## <a name="create-the-readint-activity"></a>ReadInt アクティビティを作成する

1. [**プロジェクト**] メニューの [**新しい項目の追加**] をクリックします。

2. [**インストールされている**  >  **共通項目**] ノードで、[**ワークフロー**] を選択します。 [**ワークフロー** ] の一覧から [**コードアクティビティ**] を選択します。

3. [**名前**] ボックスに「`ReadInt`」と入力して、[**追加**] をクリックします。

4. 既存の `ReadInt` 定義を次の定義に置き換えます。

     [!code-csharp[CFX_WF_GettingStarted#1](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/readint.cs#1)]
     [!code-vb[CFX_WF_GettingStarted#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/readint.vb#1)]

    > [!NOTE]
    > `ReadInt` アクティビティは、コード アクティビティ テンプレートの既定値である <xref:System.Activities.NativeActivity%601> ではなく <xref:System.Activities.CodeActivity> から派生します。 <xref:System.Activities.CodeActivity%601> は、<xref:System.Activities.Activity%601.Result%2A> 引数を介して公開される 1 つの結果がアクティビティによって提供される場合に使用できますが、<xref:System.Activities.CodeActivity%601> ではブックマークの使用がサポートされていないため、<xref:System.Activities.NativeActivity%601> が使用されます。

## <a name="create-the-prompt-activity"></a>Prompt アクティビティを作成する

1. **Ctrl** + **Shift** + **B**キーを押して、プロジェクトをビルドします。 プロジェクトをビルドすると、このプロジェクトの `ReadInt` アクティビティを使用して、この手順からカスタム アクティビティをビルドできます。

2. [**プロジェクト**] メニューの [**新しい項目の追加**] をクリックします。

3. [**インストールされている**  >  **共通項目**] ノードで、[**ワークフロー**] を選択します。 [**ワークフロー**] 一覧から [**アクティビティ**] を選択します。

4. [**名前**] ボックスに「`Prompt`」と入力して、[**追加**] をクリックします。

5. **ソリューションエクスプローラー**で [ **Prompt .xaml** ] をダブルクリックしてデザイナーに表示します (まだ表示されていない場合)。

6. アクティビティ デザイナーの左下にある [**引数**] をクリックして、[**引数**] ウィンドウを表示します。

7. [**Create Argument**] (引数の作成) をクリックします。

8. [名前] ボックスに「」と入力し、[ `BookmarkName` **方向**] ドロップダウンリストから [ **In** ] を選択します。次に、[**引数の型**] ドロップダウンリストから [**文字列**] を選択し **、enter**キーを押して引数を保存します。 **Name**

9. [**Create Argument**] (引数の作成) をクリックします。

10. `Result`新しく追加された引数の下にある [**名前**] ボックスに「」と入力し、 `BookmarkName` [**方向**] ドロップダウンリストから [ **Out** ] を選択します。次に、[**引数の型**] ドロップダウンリストから [ **Int32** ] を選択し **、enter**キーを押します。

11. [**Create Argument**] (引数の作成) をクリックします。

12. [名前] ボックスに「」と入力し、[ `Text` **方向**] ドロップダウンリストから [ **In** ] を選択します。次に、[**引数の型**] ドロップダウンリストから [**文字列**] を選択し **、enter**キーを押して引数を保存します。 **Name**

     これら 3 つの引数は、次の手順で、<xref:System.Activities.Statements.WriteLine> アクティビティに追加される `ReadInt` アクティビティと `Prompt` アクティビティの対応する引数にバインドされます。

13. アクティビティ デザイナーの左下にある [**引数**] をクリックして、[**引数**] ウィンドウを閉じます。

14. [**ツールボックス**] の [**制御フロー** ] セクションから**Sequence**アクティビティをドラッグし、 **Prompt**アクティビティデザイナーの [**ここにアクティビティをドロップ**] ラベルの上にドロップします。

    > [!TIP]
    > [**ツールパレット**] ウィンドウが表示されていない場合は、[**表示**] メニューから [**ツールパレット**] を選択します。

15. **ツールボックス**の [**プリミティブ**] セクションから**WriteLine**アクティビティをドラッグし、 **Sequence**アクティビティの [ここに**アクティビティをドロップ**] ラベルにドロップします。

16. [プロパティ] ウィンドウの [ **WriteLine** C# の式を入力するか、VB の式を入力してください] ボックスに「」と入力し、WriteLine アクティビティの**Text**引数を**Prompt**アクティビティの**text**引数にバインド `Text` します。次に、 **tab**キーを2回押します。 **Enter a C# expression** **Enter a VB expression** **Properties** これで、IntelliSense リスト メンバー ウィンドウを閉じ、プロパティから選択を外してプロパティ値を保存します。 このプロパティは `Text` 、アクティビティ自体の [C# の**式を入力**するか、 **VB の式を入力**してください] ボックスに「」と入力して設定することもできます。

    > [!TIP]
    > [**プロパティ] ウィンドウ**が表示されていない場合は、[**表示**] メニューの [**プロパティウィンドウ**] をクリックします。

17. **ツールボックス**の [ **NumberGuessWorkflowActivities** ] セクションから**readint**アクティビティをドラッグし、 **WriteLine**アクティビティに従うように**Sequence**アクティビティにドロップします。

18. [ **Prompt** **BookmarkName** **BookmarkName**プロパティ] ウィンドウで BookmarkName 引数の右にある [VB の式を入力してください] ボックスに「」と入力し、tab キーを2回押して、IntelliSense の一覧のメンバーウィンドウを閉じ、プロパティを保存して、 **Readint**アクティビティの BookmarkName 引数を Prompt アクティビティの BookmarkName 引数にバインド `BookmarkName` します。 **Enter a VB expression** **BookmarkName** **Properties Window** **Tab**

19. [ **Prompt** **Result**プロパティ**Result** ] ウィンドウで result 引数の右側にある [VB の式を入力してください] ボックスに「」と入力して、 **Readint**アクティビティの result 引数を Prompt アクティビティの result 引数にバインドし、 `Result` **tab**キーを2回押します。 **Enter a VB expression** **Result** **Properties Window**

20. **Ctrl** + **Shift** + **B**キーを押して、ソリューションをビルドします。

## <a name="next-steps"></a>次のステップ

これらのアクティビティを使用してワークフローを作成する方法については、チュートリアルの次の手順「[方法: ワークフローを作成](how-to-create-a-workflow.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Activities.CodeActivity>
- <xref:System.Activities.NativeActivity%601>
- [カスタム アクティビティの設計と実装](designing-and-implementing-custom-activities.md)
- [はじめにチュートリアル](getting-started-tutorial.md)
- [方法: ワークフローを作成する](how-to-create-a-workflow.md)
- [カスタム アクティビティ デザイナーでの ExpressionTextBox の使用](./samples/using-the-expressiontextbox-in-a-custom-activity-designer.md)
