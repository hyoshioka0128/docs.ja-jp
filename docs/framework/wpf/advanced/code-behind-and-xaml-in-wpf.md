---
title: コードビハインドと XAML
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], code-behind
- code-behind files [WPF], XAML
ms.assetid: 9df6d3c9-aed3-471c-af36-6859b19d999f
ms.openlocfilehash: 32283d5b81bf92999a97711ded13a8b533ae3028
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79145346"
---
# <a name="code-behind-and-xaml-in-wpf"></a>WPF における分離コードと XAML
<a name="introduction"></a> コードビハインドとは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページがマークアップ コンパイルされる際に、マークアップ定義オブジェクトと結合されるコードを表すために使用される用語です。 このトピックでは、コードビハインドの要件と、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のコードの代替インライン コード メカニズムについて説明します。  
  
 このトピックは、次のセクションで構成されています。  
  
- [必須コンポーネント](#Prerequisites)  
  
- [コードビハインドと XAML 言語](#codebehind_and_the_xaml_language)  
  
- [WPF のコードビハインド、イベント ハンドラー、および部分クラスの要件](#Code_behind__Event_Handler__and_Partial_Class)  
  
- [x:Code](#x_Code)  
  
- [インライン コードの制限事項](#Inline_Code_Limitations)  
  
<a name="Prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックは、[XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md) に関するページを読み、CLR とオブジェクト指向プログラミングの基本的な知識があることを前提としています。  
  
<a name="codebehind_and_the_xaml_language"></a>
## <a name="code-behind-and-the-xaml-language"></a>コードビハインドと XAML 言語  
 XAML 言語には、コード ファイルをマークアップ ファイル側からマークアップ ファイルに関連付けることができるようになる言語レベルの機能が含まれています。 具体的には、XAML 言語には言語機能 [x:Class Directive](../../../desktop-wpf/xaml-services/xclass-directive.md)、[x:Subclass Directive](../../../desktop-wpf/xaml-services/xsubclass-directive.md)、および [x:ClassModifier Directive](../../../desktop-wpf/xaml-services/xclassmodifier-directive.md) が定義されています。 コードを生成する詳細な方法と、マークアップとコードを統合する方法は、XAML 言語には規定されていません。 コードの統合方法、アプリケーションおよびプログラミング モデルでの XAML の使用方法、ビルド アクション、またはこれらすべてに必要なその他のサポートを決定するのは、WPF などのフレームワークの役割です。  
  
<a name="Code_behind__Event_Handler__and_Partial_Class"></a>
## <a name="code-behind-event-handler-and-partial-class-requirements-in-wpf"></a>WPF のコードビハインド、イベント ハンドラー、および部分クラスの要件  
  
- 部分クラスは、ルート要素をバッキングする型から派生する必要があります。  
  
- マークアップ コンパイル ビルド アクションの既定の動作では、コードビハインド側の部分クラス定義で派生を空白のままにすることができる点に注意してください。 コンパイルされた結果では、たとえ指定されていなくても、ページ ルートのバッキングの種類が部分クラスの基礎であると想定されます。 ただし、この動作に依存することはベスト プラクティスではありません。  
  
- コードビハインドで記述するイベント ハンドラーはインスタンス メソッドにする必要があります。また、静的メソッドにすることはできません。 これらのメソッドは、`x:Class` で識別される CLR 名前空間内の部分クラスによって定義する必要があります。 イベント ハンドラーの名前を修飾して、別のクラス スコープでイベント ワイヤリング用のイベント ハンドラーを探すように [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサに指示することはできません。  
  
- このハンドラーは、バッキング型システムの適切なイベントのデリゲートと一致する必要があります。  
  
- 特に Microsoft Visual Basic 言語の場合は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の属性を使用してハンドラーをアタッチするのではなく、言語固有の `Handles` キーワードを使用して、ハンドラーをハンドラー宣言のインスタンスとイベントに関連付けることができます。 ただし、この手法にはいくつかの制限事項があります。`Handles` キーワードでは、特定のルーティング イベント シナリオや添付イベントなどの [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] イベント システムの特定の機能のすべてをサポートできないためです。 詳細については、「[Visual Basic と WPF のイベント処理](visual-basic-and-wpf-event-handling.md)」を参照してください。  
  
<a name="x_Code"></a>
## <a name="xcode"></a>x:Code  
 [x:Code](../../../desktop-wpf/xaml-services/xcode-intrinsic-xaml-type.md) は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] に定義されているディレクティブ要素です。 `x:Code` ディレクティブ要素には、インライン プログラミング コードを含めることができます。 インラインで定義されたコードからは、同じページ上の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] と対話できます。 インライン C# コードの例を次に示します。 コードが `x:Code` 要素内にあり、XML のコンテンツをエスケープするには `<CDATA[`...`]]>` でコードを囲む必要があることに注意してください。これにより、([!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] スキーマまたは [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] スキーマを解釈する) [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、コンテンツは文字どおり XML として解釈されません。  
  
 [!code-xaml[XAMLOvwSupport#ButtonWithInlineCode](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page4.xaml#buttonwithinlinecode)]  
  
<a name="Inline_Code_Limitations"></a>
## <a name="inline-code-limitations"></a>インライン コードの制限事項  
 インライン コードの使用を回避または制限することを検討する必要があります。 アーキテクチャとコーディングの理念という観点から、マークアップとコードビハインドの分離を維持することで、デザイナーと開発者の役割がより明確になります。 より技術的なレベルで言うと、インライン コード用に作成するコードは作成しづらい場合があります。常に [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で生成された部分クラスに書き込み、既定の XML 名前空間マッピングしか使用できないためです。 `using` ステートメントを追加できないため、実行する API 呼び出しの多くを完全に修飾する必要があります。 既定の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] マッピングには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アセンブリに存在する CLR 名前空間のほとんどが含まれていますが、すべてではありません。他の CLR 名前空間に含まれる型とメンバーへの呼び出しは完全に修飾する必要があります。 また、インライン コードで部分クラス以外のものを定義することはできません。また、参照するすべてのユーザー コード エンティティは、生成元の部分クラス内のメンバーまたは変数として存在する必要があります。 グローバル変数またはビルド変数に対するマクロや `#ifdef` など、他の言語固有のプログラミング機能も使用できません。 詳細については、「[x:Code 組み込み XAML 型](../../../desktop-wpf/xaml-services/xcode-intrinsic-xaml-type.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [x:Code 組み込み XAML 型 ](../../../desktop-wpf/xaml-services/xcode-intrinsic-xaml-type.md)
- [WPF アプリケーションのビルド](../app-development/building-a-wpf-application-wpf.md)
- [XAML 構文の詳細](xaml-syntax-in-detail.md)
