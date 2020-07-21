---
title: XamlWriter.Save のシリアル化の制限
ms.date: 03/30/2017
helpviewer_keywords:
- XamlWriter.Save [WPF], serialization limitations of
- limitations of XamlWriter.Save
- serialization limitations of XamlWriter.Save
ms.assetid: f86acc91-2b67-4039-8555-505734491d36
ms.openlocfilehash: 96e917898320fb5d49f4e7dfc27daa7750af9d41
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174369"
---
# <a name="serialization-limitations-of-xamlwritersave"></a>XamlWriter.Save のシリアル化の制限
API <xref:System.Windows.Markup.XamlWriter.Save%2A> は、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションのコンテンツを [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ファイルとしてシリアル化するために使用できます。 ただし、何がシリアル化されるかについては、いくつかの重要な制限事項があります。 このトピックでは、これらの制限事項と、いくつかの一般的な考慮事項について説明します。  

<a name="Run_Time__Not_Design_Time_Representation"></a>
## <a name="run-time-not-design-time-representation"></a>実行時の表現 (デザイン時ではなく)  
 <xref:System.Windows.Markup.XamlWriter.Save%2A> の呼び出しによって何がシリアル化されるのかについて、基本的に言えることは、結果として得られるのが、実行時にシリアル化されるオブジェクトの表現であるということです。 元の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルのデザイン時プロパティの多くは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] がメモリ内オブジェクトとして読み込まれる時に既に最適化されているか、または失われている可能性があるため、<xref:System.Windows.Markup.XamlWriter.Save%2A> を呼び出してシリアル化する際には保持されません。 シリアル化された結果は、アプリケーションの構築済みの論理ツリーを効果的に表現したものですが、それを生成した元の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] であるとは限りません。 これらの問題があるため、<xref:System.Windows.Markup.XamlWriter.Save%2A> によるシリアル化を [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の広範なデザイン サーフェイスの一部として使用することは非常に困難となっています。  
  
<a name="Serialization_is_Self_Contained"></a>
## <a name="serialization-is-self-contained"></a>シリアル化は自己完結型  
 <xref:System.Windows.Markup.XamlWriter.Save%2A> のシリアル化出力は自己完結型です。シリアル化されるすべてのものは、1 つのルート要素を持つ単一の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページに含まれ、URI 以外の外部参照は含まれません。 たとえば、アプリケーション リソースからリソースを参照しているページの場合、それらのリソースは、シリアル化されたページのコンポーネントであるかのように表示されます。  
  
<a name="Extension_References_are_Dereferenced"></a>
## <a name="extension-references-are-dereferenced"></a>拡張機能の参照は逆参照される  
 さまざまなマークアップ拡張形式によって行われるオブジェクトへの一般的な参照 (`StaticResource` や `Binding` など) は、シリアル化プロセスによって逆参照されます。 これらは、メモリ内オブジェクトがアプリケーション ランタイムによって作成された時点で既に逆参照されており、<xref:System.Windows.Markup.XamlWriter.Save%2A> ロジックでは、元の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を再参照して、それらの参照をシリアル化出力に復元することはしません。 そのため、データバインドされた値やリソースで取得される値は、実行時の表現で最後に使用された値になる可能性があります。したがって、それらの値をローカルで設定されたその他の値と区別することは、部分的または間接的にしかできなくなります。 また、イメージは、元のソースの参照としてではなく、プロジェクト内に存在するイメージへのオブジェクト参照としてシリアル化されるため、当初参照されたファイル名や URI は失われます。 同じページ内で宣言されたリソースであっても、リソース コレクションのキーとして保存されるのではなく、それらが参照されたポイントへとシリアル化されます。  
  
<a name="Event_Handling_is_Not_Preserved"></a>
## <a name="event-handling-is-not-preserved"></a>イベント処理は保持されない  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] によって追加されたイベント ハンドラーがシリアル化された場合、それらは保持されません。 分離コードを使用しない (関連する x:Code 機構もない) [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、ランタイムのプロシージャ ロジックをシリアル化することができません。 シリアル化は自己完結型であり、論理ツリーに限定されているため、イベント ハンドラーを格納する機能はありません。 そのため、イベント ハンドラー属性は、属性自体も、またハンドラーに名前を付ける文字列値も、出力後の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] からは削除されます。  
  
<a name="Realistic_Scenarios_for_Use_of_XAMLWriter_Save"></a>
## <a name="realistic-scenarios-for-use-of-xamlwritersave"></a>XAMLWriter.Save の現実的な利用シナリオ  
 以上のように、<xref:System.Windows.Markup.XamlWriter.Save%2A> を使ったシリアル化にはかなりの制限事項が伴いますが、これを使用する適切なシナリオもいくつか存在します。  
  
- ベクターまたはグラフィカル出力:レンダリングされた領域の出力を使用して、再読み込み時に同じベクターやグラフィックスを再現できます。  
  
- リッチ テキストおよびフロー ドキュメント:テキストと、その中の要素書式設定や要素含有はすべて、出力内に保持されます。 これは、クリップボードのような機能を提供するのに役立ちます。  
  
- ビジネス オブジェクト データの保持:カスタム要素に格納されているデータ (XML データなど) がある場合、ビジネス オブジェクトが、基本的な [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ルール (カスタム コンストラクターの提供や、参照渡しのプロパティ値に対応した変換など) に従っていれば、それらのビジネス オブジェクトをシリアル化によって永続化できます。
