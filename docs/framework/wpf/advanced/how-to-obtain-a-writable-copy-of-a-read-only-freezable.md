---
title: '方法: 読み取り専用の Freezable の書き込み可能なコピーを取得する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cloning Freezable objects [WPF]
- Freezable objects [WPF], modifiable clones
ms.assetid: d028de61-bbe9-4d62-b656-8fe3b1b2ca24
ms.openlocfilehash: 910c5dada6ca82f68992722e4df6b35f9f7497c7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61942793"
---
# <a name="how-to-obtain-a-writable-copy-of-a-read-only-freezable"></a>方法: 読み取り専用の Freezable の書き込み可能なコピーを取得する
この例では、<xref:System.Windows.Freezable.Clone%2A> メソッドを使用して、読み取り専用の <xref:System.Windows.Freezable> の書き込み可能なコピーを作成する方法を示します。  
  
 <xref:System.Windows.Freezable> オブジェクトを読み取り専用 ("固定") としてマークした後は、そのオブジェクトを変更することはできません。 ただし、<xref:System.Windows.Freezable.Clone%2A> メソッドを使用すると、固定オブジェクトの複製を作成して、それを変更することができます。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Media.SolidColorBrush> の固定オブジェクトの変更可能な複製を作成します。  
  
 [!code-csharp[freezablesample_procedural#CloneExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
 [!code-vb[freezablesample_procedural#CloneExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]  
  
 <xref:System.Windows.Freezable> オブジェクトの詳細については、「[Freezable オブジェクトの概要](freezable-objects-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Freezable>
- <xref:System.Windows.Freezable.CloneCurrentValue%2A>
- [Freezable オブジェクトの概要](freezable-objects-overview.md)
- [方法トピック](base-elements-how-to-topics.md)
