---
title: '方法: インク データにカスタム データを追加する'
ms.date: 03/30/2017
helpviewer_keywords:
- ink data [WPF], adding custom data
- InkCanvas [WPF], displaying
ms.assetid: f02aac6f-3436-4f7c-b6ea-0452cba5332c
ms.openlocfilehash: 7c59a205df5358daec101339cc6a308c8e38a9d6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64640867"
---
# <a name="how-to-add-custom-data-to-ink-data"></a>方法: インク データにカスタム データを追加する
インクが Ink Serialized Format (ISF) として保存されるときに、保存されるインクにカスタム データを追加できます。  カスタム データは、<xref:System.Windows.Ink.DrawingAttributes>、<xref:System.Windows.Ink.StrokeCollection>、または <xref:System.Windows.Ink.Stroke> に保存できます。  カスタム データは 3 つのオブジェクトに保存できるため、データを保存する最適な場所を決めることができます。  これら 3 つのクラスすべてで同様のメソッドを使用し、カスタム データの格納とアクセスが行われます。  
  
 カスタム データとして保存できるのは、次の種類のみとなります。  
  
- <xref:System.Boolean>  
  
- <xref:System.Boolean>[]  
  
- <xref:System.Byte>  
  
- <xref:System.Byte>[]  
  
- <xref:System.Char>  
  
- <xref:System.Char>[]  
  
- <xref:System.DateTime>  
  
- <xref:System.DateTime>[]  
  
- <xref:System.Decimal>  
  
- <xref:System.Decimal>[]  
  
- <xref:System.Double>  
  
- <xref:System.Double>[]  
  
- <xref:System.Int16>  
  
- <xref:System.Int16>[]  
  
- <xref:System.Int32>  
  
- <xref:System.Int32>[]  
  
- <xref:System.Int64>  
  
- <xref:System.Int64>[]  
  
- <xref:System.Single>  
  
- <xref:System.Single>[]  
  
- <xref:System.String>  
  
- <xref:System.UInt16>  
  
- <xref:System.UInt16>[]  
  
- <xref:System.UInt32>  
  
- <xref:System.UInt32>[]  
  
- <xref:System.UInt64>  
  
- <xref:System.UInt64>[]  
  
## <a name="example"></a>例  
 次の例は、<xref:System.Windows.Ink.StrokeCollection> に対してカスタム データの追加および取得を行う方法を示しています。  
  
 [!code-csharp[HowToAddCustomDataToInk#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#1)]  
  
 次の例では、<xref:System.Windows.Controls.InkCanvas> と 2 つのボタンを表示するアプリケーションを作成します。  ボタン `switchAuthor` により、2 人の別々の作成者が 2 つのペンを使用できるようになります。  ボタン `changePenColors` により、<xref:System.Windows.Controls.InkCanvas> 上の各ストロークの色が作成者に応じて変更されます。  このアプリケーションでは、2 つの <xref:System.Windows.Ink.DrawingAttributes> オブジェクトが定義され、<xref:System.Windows.Ink.Stroke> を描画した作成者を示すカスタム プロパティがそれぞれに追加されます。  ユーザーが `changePenColors` をクリックすると、アプリケーションによって、ストロークの外観がカスタム プロパティの値に従って変更されます。  
  
 [!code-xaml[HowToAddCustomDataToInk#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[HowToAddCustomDataToInk#3](~/samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#3)]
