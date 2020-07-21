---
title: '方法: 装飾を実装する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], implementing
ms.assetid: 56ae32b6-0599-455c-b52f-2ff97e6f1ec2
ms.openlocfilehash: da318fee42b4628351217774de2a2225cfb21ee1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770982"
---
# <a name="how-to-implement-an-adorner"></a>方法: 装飾を実装する
この例は、最小限の装飾の実装を示しています。  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 装飾自体にはレンダリング動作が備わっていないので、装飾のレンダリングは装飾の実装側の責任で行う必要がある点に、注意が必要です。   レンダリング動作を実装する一般的な方法は、(この例で示すように) <xref:System.Windows.UIElement.OnRender%2A> メソッドをオーバーライドし、1 つまたは複数の <xref:System.Windows.Media.DrawingContext> オブジェクトを使用して、必要に応じて装飾のビジュアルをレンダリングすることです。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 抽象型 <xref:System.Windows.Documents.Adorner> クラスから継承されるクラスを実装することにより、カスタム装飾が作成されます。  この例の装飾は、<xref:System.Windows.UIElement.OnRender%2A> メソッドをオーバーライドすることで <xref:System.Windows.UIElement> の四隅を円で装飾するだけのものです。  
  
### <a name="code"></a>コード  
 [!code-csharp[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_simplecircleadornerbody)]
 [!code-vb[Adorners_SimpleCircleAdorner#_SimpleCircleAdornerBody](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_simplecircleadornerbody)]  
  
## <a name="see-also"></a>関連項目

- [装飾の概要](adorners-overview.md)
