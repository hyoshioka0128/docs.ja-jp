---
title: XAML 読み込みと依存関係プロパティ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom dependency properties [WPF]
- dependency properties [WPF], XAML loading and
- loading XML data [WPF]
ms.assetid: 6eea9f4e-45ce-413b-a266-f08238737bf2
ms.openlocfilehash: de8050e582f5b1a5a288c350c179cfa24fb5471c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186248"
---
# <a name="xaml-loading-and-dependency-properties"></a>XAML 読み込みと依存関係プロパティ
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] での [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサの現在の実装では、本質的に依存関係プロパティが認識されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、バイナリ [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を読み込み、依存関係プロパティである属性を処理するときに、依存関係プロパティに対するプロパティ システム メソッドが使用されます。 これにより、プロパティ ラッパーは実質的にバイパスされます。 カスタム依存関係プロパティを実装するときは、この動作について考慮する必要があります。また、プロパティ ラッパーには、プロパティ システム メソッド <xref:System.Windows.DependencyObject.GetValue%2A> および <xref:System.Windows.DependencyObject.SetValue%2A> 以外の他のコードを配置しないようにする必要があります。  

<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックは、利用者と作成者の両方として依存関係プロパティを理解しており、「[依存関係プロパティの概要](dependency-properties-overview.md)」と「[カスタム依存関係プロパティ](custom-dependency-properties.md)」を読んでいることを前提としています。 また、「[XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)」と「[XAML 構文の詳細](xaml-syntax-in-detail.md)」も読んでおく必要があります。  
  
<a name="implementation"></a>
## <a name="the-wpf-xaml-loader-implementation-and-performance"></a>WPF XAML ローダーの実装とパフォーマンス  
 実装上の理由から、プロパティ ラッパーとそのセッターを使用するのではなく、プロパティを依存関係プロパティとして識別し、プロパティ システムの <xref:System.Windows.DependencyObject.SetValue%2A> メソッドを使用してプロパティを設定する方が、計算がより低コストになります。 これは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のプロセッサでは、マークアップとさまざまな文字列の構造によって示される型とメンバーの関係に関する知識だけに基づいて、バッキング コードのオブジェクト モデル全体を推測する必要があるためです。  
  
 型は xmlns 属性と assembly 属性の組み合わせによって参照されますが、メンバーを識別し、属性として設定できるサポートを判断し、プロパティ値でサポートされる型を解決するには、<xref:System.Reflection.PropertyInfo> を使用する広範なリフレクションが必要です。 特定の型に対する依存関係プロパティには、プロパティ システムを通じてストレージ テーブルとしてアクセスできるため、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] による [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサの実装では、このテーブルが使用され、依存関係プロパティ識別子 *ABCProperty* を使用して、包含する <xref:System.Windows.DependencyObject> 派生型で <xref:System.Windows.DependencyObject.SetValue%2A> を呼び出すことにより、特定のプロパティ *ABC* をより効率的に設定できることが推測されます。  
  
<a name="implications"></a>
## <a name="implications-for-custom-dependency-properties"></a>カスタム依存関係プロパティに対する影響  
 現在の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によるプロパティ設定に対する [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサ動作の実装では、ラッパーが完全にバイパスされるため、カスタム依存関係プロパティのラッパーの set 定義に追加のロジックを含めないでください。 そのようなロジックを set 定義に含めた場合、プロパティがコードではなく [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で設定されていると、ロジックは実行されません。  
  
 同様に、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 処理からプロパティ値を取得する [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサのその他の側面でも、ラッパーを使用するのではなく、<xref:System.Windows.DependencyObject.GetValue%2A> が使用されます。 したがって、`get` 定義でも、<xref:System.Windows.DependencyObject.GetValue%2A> の呼び出し以外のものを追加して実装しないようにする必要があります。  
  
 次の例は、ラッパーでの依存関係プロパティの推奨される定義です。ここでは、プロパティ識別子は `public` `static` `readonly` フィールドとして格納されており、`get` と `set` の定義には、依存関係プロパティのバッキングを定義する必要なプロパティ システム メソッド以外のコードは含まれていません。  
  
 [!code-csharp[WPFAquariumSln#AGWithWrapper](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#agwithwrapper)]
 [!code-vb[WPFAquariumSln#AGWithWrapper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#agwithwrapper)]  
  
## <a name="see-also"></a>関連項目

- [依存関係プロパティの概要](dependency-properties-overview.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [依存関係プロパティのメタデータ](dependency-property-metadata.md)
- [コレクション型依存関係プロパティ](collection-type-dependency-properties.md)
- [依存関係プロパティのセキュリティ](dependency-property-security.md)
- [DependencyObject の安全なコンストラクター パターン](safe-constructor-patterns-for-dependencyobjects.md)
