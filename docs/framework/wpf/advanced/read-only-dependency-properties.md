---
title: 読み取り専用の依存関係プロパティ
ms.date: 03/30/2017
helpviewer_keywords:
- dependency properties [WPF], read-only
- read-only dependency properties [WPF]
ms.assetid: f23d6ec9-3780-4c09-a2ff-b2f0a2deddf1
ms.openlocfilehash: 8adc90182f0f42f52e6ace4e13c68acb3539516b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187181"
---
# <a name="read-only-dependency-properties"></a>読み取り専用の依存関係プロパティ
このトピックでは、既存の読み取り専用の依存関係プロパティ、カスタムの読み取り専用の依存関係プロパティを作成するシナリオと手法など、読み取り専用の依存関係プロパティについて説明します。  

<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックでは、依存関係プロパティの実装の基本シナリオとカスタム依存関係プロパティへのメタデータの適用方法を理解していることを前提とします。 詳細については、「[カスタム依存関係プロパティ](custom-dependency-properties.md)」および「[依存関係プロパティのメタデータ](dependency-property-metadata.md)」を参照してください。  
  
<a name="existing"></a>
## <a name="existing-read-only-dependency-properties"></a>既存の読み取り専用の依存関係プロパティ  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] フレームワークで定義されている依存関係プロパティの一部は読み取り専用です。 読み取り専用の依存関係プロパティを指定する一般的な理由は、それらが状態決定に使用されるプロパティであるにも関わらず、その状態は多くの要因の影響を受け、プロパティをその状態に設定するだけではユーザー インターフェイス設計の観点から望ましくないことにあります。 たとえば、プロパティ <xref:System.Windows.UIElement.IsMouseOver%2A> はマウス入力で決定される表示上の状態に過ぎません。 実際にマウス入力を行わずにプログラムでこの値を設定しようとすると、予期しない結果になり、不整合が生じる原因になります。  
  
 設定可能ではないため、読み取り専用の依存関係プロパティは、依存関係プロパティがソリューションを通常提供するシナリオの多くには適切ではありません (データ バインディング、直接スタイル設定可能な値、検証、アニメーション、継承など)。 それでも、設定不可能な読み取り専用依存関係プロパティには、プロパティ システムの依存関係プロパティによってサポートされるいくつかの追加機能があります。 その他の機能のうち最も重要なのは、読み取り専用の依存関係プロパティはスタイルのプロパティ トリガーとして使用できることです。 通常の共通言語ランタイム (CLR) プロパティではトリガーを有効にできません。依存関係プロパティであることが必要です。 上記の <xref:System.Windows.UIElement.IsMouseOver%2A> プロパティは、コントロールのスタイルを定義するのが便利なシナリオのよい例です。コントロール内の複合要素の背景や前景のような一部の表示関連のプロパティは、コントロールの定義済み領域をユーザーがマウスでポイントすると変化します。 読み取り専用の依存関係プロパティの変化は、プロパティ システム固有の無効化プロセスによって検出して報告することもでき、これは実際にはプロパティ トリガー機能を内部的にサポートします。  
  
<a name="new"></a>
## <a name="creating-custom-read-only-dependency-properties"></a>読み取り専用のカスタム依存関係プロパティの作成  
 多くの一般的な依存関係プロパティのシナリオで読み取り専用依存関係プロパティが機能しない理由に関する前のセクションを参照してください。 ただし、適切なシナリオがある場合は、独自の読み取り専用依存関係プロパティを作成してもかまいません。  
  
 読み取り専用の依存関係プロパティを作成するプロセスの大部分は、「[カスタム依存関係プロパティ](custom-dependency-properties.md)」と「[依存関係プロパティの実装](how-to-implement-a-dependency-property.md)」のトピックの説明と同じです。 ただし、次の 3 つの重要な違いがあります。  
  
- プロパティを登録するときは、プロパティ登録用の通常の <xref:System.Windows.DependencyProperty.Register%2A> メソッドではなく、<xref:System.Windows.DependencyProperty.RegisterReadOnly%2A> メソッドを呼び出します。  
  
- CLR の "ラッパー" プロパティを実装するときは、公開するパブリック ラッパーの読み取り専用状態が矛盾しないよう、ラッパーにも set を実装しないようにする必要があります。  
  
- 読み取り専用の登録によって返されるオブジェクトは、<xref:System.Windows.DependencyProperty> ではなく <xref:System.Windows.DependencyPropertyKey> です。 やはりこのフィールドをメンバーとして格納する必要がありますが、通常は、型のパブリック メンバーにはしません。  
  
 読み取り専用の依存関係プロパティを補足するために使用するプライベートのフィールドまたは値はすべて、適当なロジックを使用して完全に書き込み可能にしてかまいません。 ただし、初期化で、またはランタイム ロジックの一部として、プロパティを設定する最も簡単な方法は、プロパティ システムを使用しないでプライベートなバッキング フィールドを直接設定するのではなく、プロパティ システムの API を使用する方法です。 具体的には、<xref:System.Windows.DependencyPropertyKey> 型のパラメーターを受け取る <xref:System.Windows.DependencyObject.SetValue%2A> のシグネチャがあります。 アプリケーション ロジック内でプログラムによってこの値を設定する方法と場所により、依存関係プロパティを最初に登録したときに作成される <xref:System.Windows.DependencyPropertyKey> に対するアクセスの設定方法が影響を受けます。 このロジックすべてをクラス内で処理する場合はプライベートにでき、アセンブリの他の部分から設定する必要がある場合は内部に設定します。 1 つの方法は、格納されているプロパティ値の変更が必要であることをクラスのインスタンスに通知する関連イベントのクラス イベント ハンドラー内で、<xref:System.Windows.DependencyObject.SetValue%2A> を呼び出すというものです。 もう 1 つの方法は、登録のときにプロパティのメタデータの一部として、ペアになった <xref:System.Windows.PropertyChangedCallback> コールバックと <xref:System.Windows.CoerceValueCallback> コールバックを使用して、依存関係プロパティを結び付けるというものです。  
  
 <xref:System.Windows.DependencyPropertyKey> はプライベートであり、コードの外部のプロパティ システムによっては伝達されないので、読み取り専用の依存関係プロパティの方が、読み取り/書き込み依存関係プロパティより設定のセキュリティが優れています。 読み取り/書き込み依存関係プロパティの場合は、識別するフィールドは明示的または暗黙的にパブリックであり、したがってプロパティは広範に設定可能です。 詳細については、「[依存関係プロパティのセキュリティ](dependency-property-security.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [依存関係プロパティの概要](dependency-properties-overview.md)
- [カスタム依存関係プロパティ](custom-dependency-properties.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
