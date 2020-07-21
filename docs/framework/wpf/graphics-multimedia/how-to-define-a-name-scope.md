---
title: '方法: 名前のスコープを定義する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- name scope [WPF], defining
- Storyboards [WPF], animating in procedural code
- animation [WPF], Storyboards [WPF], in procedural code
ms.assetid: 4f361925-6a08-40dc-8231-a61111c6b28b
ms.openlocfilehash: a03f477dd31909e8cb9dde9cd29da6f38d665758
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904151"
---
# <a name="how-to-define-a-name-scope"></a>方法: 名前のスコープを定義する
コードで <xref:System.Windows.Media.Animation.Storyboard> を使用してアニメーション化を行うには、<xref:System.Windows.NameScope> を作成し、その名前のスコープを所有する要素にターゲット オブジェクトの名前を登録する必要があります。 次の例では、`myMainPanel` に <xref:System.Windows.NameScope> が作成されています。 パネルには、`button1` と `button2` の 2 つのボタンが追加され、その名前が登録されています。 いくつかのアニメーションと <xref:System.Windows.Media.Animation.Storyboard> が作成されています。 アニメーションの開始には、ストーリーボードの <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドが使用されています。  
  
 `button1`、`button2`、および `myMainPanel` の名前のスコープは同じであるため、そのいずれかと <xref:System.Windows.Media.Animation.Storyboard><xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドを使用して、アニメーションを開始できます。  
  
## <a name="example"></a>例  
 [!code-csharp[StoryboardBeginAnimation_procedural_snip#NameScopeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/StoryboardBeginAnimation_procedural_snip/CSharp/ScopeExample.cs#namescopeexample)]
 [!code-vb[StoryboardBeginAnimation_procedural_snip#NameScopeExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StoryboardBeginAnimation_procedural_snip/visualbasic/scopeexample.vb#namescopeexample)]  
  
## <a name="see-also"></a>関連項目

- [ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)
- [アニメーションの概要](animation-overview.md)
