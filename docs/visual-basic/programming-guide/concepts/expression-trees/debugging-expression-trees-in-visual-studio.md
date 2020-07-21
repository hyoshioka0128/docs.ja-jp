---
title: 式ツリーのデバッグ (Visual Studio)
ms.date: 07/20/2015
ms.assetid: 492cc28f-b7a2-4c47-b582-b3c437b8a5d5
ms.openlocfilehash: 3811958353d1d55ce74da41c6a45dbe730cc9790
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84375435"
---
# <a name="debugging-expression-trees-in-visual-studio-visual-basic"></a>式ツリーのデバッグ (Visual Studio) (Visual Basic)
アプリケーションをデバッグするときに、式ツリーの構造および内容を分析できます。 式ツリーの構造の概要を簡単に取得するには、`DebugView` プロパティ使用できます。このプロパティでは、[特殊な構文を使って](debugview-syntax.md)式ツリーが表されます。 (`DebugView` はデバッグ モードでのみ使用できることに注意してください。)  

![式ツリーの DebugView のスクリーンショット。](media/debugging-expression-trees-in-visual-studio/debugview-visual-basic.png)

`DebugView` は文字列なので、[組み込まれているテキスト ビジュアライザー](https://docs.microsoft.com/visualstudio/debugger/view-strings-visualizer#open-a-string-visualizer)を使って、複数行で表示できます。**テキスト ビジュアライザー**を使うには、`DebugView` ラベルの隣にある虫眼鏡アイコンから選択します。

 ![DebugView の結果に適用されるテキスト ビジュアライザーのスクリーンショット。](media/debugging-expression-trees-in-visual-studio/string-visualizer-vb.png)

または、式ツリー用の[カスタム ビジュアライザー](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data)をインストールして使うこともできます。例:

- [ReadableExpressions](https://github.com/agileobjects/ReadableExpressions) ([MIT ライセンス](https://github.com/agileobjects/ReadableExpressions/blob/master/LICENSE.md)、[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=vs-publisher-1232914.ReadableExpressionsVisualizers) で使用可能): 式ツリーがテーマを設定できる C# コードとしてレンダリングされます。さまざまなレンダリング オプションがあります。

  ![Readable Expressions Visualizer のスクリーンショット。](media/debugging-expression-trees-in-visual-studio/readable-expressions-visualizer.png)

- [Expression Tree Visualizer](https://github.com/zspitz/ExpressionTreeVisualizer/blob/master/README.md) ([MIT ライセンス](https://github.com/zspitz/ExpressionTreeVisualizer/blob/master/LICENSE)) では、式ツリーとその個々のノードのツリー ビューが提供されます。また、Visual Basic の構文を使用して式ツリーをレンダリングできます。

  ![Expression Tree Visualizer のスクリーンショット。](media/debugging-expression-trees-in-visual-studio/expression-tree-visualizer-vb.png)

### <a name="to-open-a-visualizer-for-an-expression-tree"></a>式ツリーのビジュアライザーを開くには  
  
1. **[データヒント]** 、 **[ウォッチ]** ウィンドウ、 **[自動変数]** ウィンドウ、または **[ローカル]** ウィンドウで、式ツリーの横に表示されている虫眼鏡のアイコンをクリックします。  
  
    使用可能なビジュアライザーの一覧が表示されます。

    ![Visual Studio からビジュアライザーを開くユーザーの操作を示すスクリーンショット。](media/debugging-expression-trees-in-visual-studio/expression-tree-visualizers-vb.png)

2. 使用するビジュアライザーをクリックします。  

## <a name="see-also"></a>関連項目

- [式ツリー (Visual Basic)](index.md)
- [Visual Studio でのデバッグ](/visualstudio/debugger/debugger-feature-tour)
- [カスタム ビジュアライザーを作成する](/visualstudio/debugger/create-custom-visualizers-of-data)
- [`DebugView` 構文](debugview-syntax.md)
