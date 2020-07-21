---
title: '方法: 依存関係プロパティを実装する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dependency properties [WPF], backing properties with
- properties [WPF], backing with dependency properties
ms.assetid: 855fd6d7-19ac-493c-bf5e-2f40b57cdc92
ms.openlocfilehash: 6f2fb9b0824feb6253527de063f58da2427d0c06
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2019
ms.locfileid: "68400355"
---
# <a name="how-to-implement-a-dependency-property"></a>方法: 依存関係プロパティを実装する
この例では、共通言語ランタイム (CLR) プロパティを <xref:System.Windows.DependencyProperty> フィールドで補足し、依存関係プロパティを定義する方法を示します。 独自に定義したプロパティが [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のさまざまな機能、たとえばスタイル、データ バインディング、継承、アニメーション、既定値をサポートできるようにするには、そのプロパティを依存関係プロパティとして実装します。  
  
## <a name="example"></a>例  
 次の例では、最初に <xref:System.Windows.DependencyProperty.Register%2A> メソッドを呼び出して依存関係プロパティを登録します。 依存関係プロパティの名前と特性を格納するときに使用する識別子フィールドの名前は、<xref:System.Windows.DependencyProperty.Register%2A> の呼び出しの一部として依存関係プロパティに対して選択した <xref:System.Windows.DependencyProperty.Name%2A> に、リテラル文字列 `Property` が付加されたものである必要がありますます。 たとえば、登録する依存関係プロパティの <xref:System.Windows.DependencyProperty.Name%2A> が `Location` ならば、この依存関係プロパティに対して定義する識別子フィールドの名前は `LocationProperty` とする必要があります。  
  
 この例では、依存関係プロパティとその CLR アクセサーの名前は `State`、識別子フィールドは `StateProperty`、プロパティの型は <xref:System.Boolean>、依存関係プロパティを登録する型は `MyStateControl` です。  
  
 このパターンに従って名前が付けられていない場合は、定義したプロパティがデザイナーから正しく報告されず、プロパティ システムのスタイル適用の一部が予期したとおりに動作しなくなる可能性があります。  
  
 依存関係プロパティの既定のメタデータを指定することもできます。 `State` 依存関係プロパティの既定値を `false` として登録する例を次に示します。  
  
 [!code-csharp[PropertySystemEsoterics#MyStateControl](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertySystemEsoterics/CSharp/SDKSampleLibrary/class1.cs#mystatecontrol)]
 [!code-vb[PropertySystemEsoterics#MyStateControl](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertySystemEsoterics/visualbasic/sdksamplelibrary/class1.vb#mystatecontrol)]  
  
 単にプライベート フィールドを使用して CLR プロパティを補足するのではなく依存関係プロパティを実装する理由とその方法の詳細については、「[依存関係プロパティの概要](dependency-properties-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [依存関係プロパティの概要](dependency-properties-overview.md)
- [方法トピック](properties-how-to-topics.md)
