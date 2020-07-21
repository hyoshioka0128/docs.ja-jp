---
title: '方法: Freezable を読み取り専用にする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Freezable objects [WPF], making read-only
ms.assetid: 6c544b7d-d3c9-4736-aa90-4b8728234ccb
ms.openlocfilehash: 4185966d864be425bc631953461f6f27ab983bee
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73460071"
---
# <a name="how-to-make-a-freezable-read-only"></a>方法: Freezable を読み取り専用にする
この例では、<xref:System.Windows.Freezable.Freeze%2A> メソッドを呼び出して <xref:System.Windows.Freezable> を読み取り専用にする方法を示します。  
  
 オブジェクトについて次のいずれかの条件が `true` の場合、<xref:System.Windows.Freezable> オブジェクトを凍結することはできません。  
  
- アニメーション化されたプロパティまたはデータ バインドされたプロパティがあります。  
  
- 動的リソースによって設定されるプロパティがあります。 動的リソースの詳細については、[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。  
  
- 凍結できない <xref:System.Windows.Freezable> サブオブジェクトが含まれています。  
  
 <xref:System.Windows.Freezable> オブジェクトに対して、これらの条件が `false` であり、このオブジェクトを変更する予定がない場合は、パフォーマンスを向上させるために凍結させることを検討してください。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Freezable> オブジェクトの型である <xref:System.Windows.Media.SolidColorBrush> を凍結します。  
  
 [!code-csharp[freezablesample_procedural#FreezeExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#freezeexample1)]
 [!code-vb[freezablesample_procedural#FreezeExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#freezeexample1)]  
  
 <xref:System.Windows.Freezable> オブジェクトの詳細については、「[Freezable オブジェクトの概要](freezable-objects-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Freezable>
- <xref:System.Windows.Freezable.CanFreeze%2A>
- <xref:System.Windows.Freezable.Freeze%2A>
- [Freezable オブジェクトの概要](freezable-objects-overview.md)
- [方法トピック](base-elements-how-to-topics.md)
