---
title: フレームワーク プロパティ メタデータ
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WPF], framework properties
- framework property metadata [WPF]
ms.assetid: 9962f380-b885-4b61-a62e-457397083fea
ms.openlocfilehash: 8fb6e1b4cf6aed9454e9e9f1a77277d2f3611ca8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186656"
---
# <a name="framework-property-metadata"></a>フレームワーク プロパティ メタデータ
フレームワーク プロパティ メタデータのオプションは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アーキテクチャの WPF フレームワーク レベルにあると見なされるオブジェクト要素のプロパティに対して報告されます。 一般に、WPF フレームワーク レベルが指定されている場合、レンダリング、データ バインディング、プロパティ システムの調整などの機能は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のプレゼンテーション API と実行可能ファイルによって処理されます。 フレームワーク プロパティ メタデータがこれらのシステムによって照会されて、特定の要素プロパティに対する機能固有の特性が決まります。  

<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックでは、ユーザーが [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] クラスの既存の依存関係プロパティの使用という観点から依存関係プロパティを理解し、「[依存関係プロパティの概要](dependency-properties-overview.md)」トピックを通読していることを前提としています。 また、「[依存関係プロパティのメタデータ](dependency-property-metadata.md)」を読んでいる必要もあります。  
  
<a name="What_Is_Communicated_by_Framework_Property"></a>
## <a name="what-is-communicated-by-framework-property-metadata"></a>フレームワーク プロパティ メタデータによる通知内容  
 フレームワーク プロパティ メタデータは、次のように分類できます。  
  
- 要素に影響するレイアウト プロパティの報告 (<xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A>、<xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A>、<xref:System.Windows.FrameworkPropertyMetadata.AffectsRender%2A>)。 プロパティがそれぞれの側面に影響する場合、メタデータにこれらのフラグを設定できます。また、<xref:System.Windows.FrameworkElement.MeasureOverride%2A> / <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> メソッドをクラスに実装して、特定のレンダリングの動作と情報をレイアウト システムに指定します。 通常、そのような実装では、依存関係プロパティのメタデータでこれらのレイアウト プロパティのいずれかが true であると、プロパティの無効化があるかどうかがチェックされます。無効化があった場合にのみ、新しいレイアウト パスの要求が必要となります。  
  
- 要素の親要素に影響するレイアウト プロパティの報告 (<xref:System.Windows.FrameworkPropertyMetadata.AffectsParentArrange%2A>、<xref:System.Windows.FrameworkPropertyMetadata.AffectsParentMeasure%2A>)。 これらのフラグが既定で設定される例は、<xref:System.Windows.Documents.FixedPage.Left%2A?displayProperty=nameWithType> や <xref:System.Windows.Documents.Paragraph.KeepWithNext%2A?displayProperty=nameWithType> などです。  
  
- <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A>。 既定では、依存関係プロパティは値を継承しません。 <xref:System.Windows.FrameworkPropertyMetadata.OverridesInheritanceBehavior%2A> を使用すると、継承のパスがビジュアル ツリー内を通ることもできるようになります。コントロールを複合する一部のシナリオでは、このような必要が生じることがあります。  
  
    > [!NOTE]
    > プロパティ値のコンテキストにおける "継承" という用語は、依存関係プロパティに固有の事項を意味します。つまり、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プロパティ システムの WPF フレームワーク レベルの機能によって、実際の依存関係プロパティ値を子要素が親要素から継承できることを意味します。 派生型を通じたマネージド コードの型およびメンバーの継承とは直接関係はありません。 詳細については、「[プロパティ値の継承](property-value-inheritance.md)」を参照してください。  
  
- データ バインディング特性の報告 (<xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A>、<xref:System.Windows.FrameworkPropertyMetadata.BindsTwoWayByDefault%2A>)。 既定では、フレームワークの依存関係プロパティは、一方向のバインディング動作を持つデータ バインディングをサポートします。 必要がない場合はデータ バインディングを無効にできます (柔軟性と拡張性を目的とするため、既定の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] API にそのようなプロパティの例は多くありません)。 複数のコンポーネント間でコントロールの動作を関連付けるプロパティ (<xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> など) や、ユーザーにとって双方向のバインディングが一般的かつ期待されるシナリオであるプロパティ (<xref:System.Windows.Controls.TextBox.Text%2A> など) に対しては、双方向のバインディングを既定として設定できます。 データ バインディング関連のメタデータを変更した場合に影響を受けるのは既定値だけです。この既定値は、バインディングごとにいつでも変更できます。 バインディング モードおよびバインディング全般の詳細については、「[データ バインドの概要](../../../desktop-wpf/data/data-binding-overview.md)」を参照してください。  
  
- ジャーナリングをサポートするアプリケーションまたはサービスによって、プロパティをジャーナリングするかどうかの報告 (<xref:System.Windows.FrameworkPropertyMetadata.Journal%2A>)。 一般的な要素に対しては、ジャーナリングは既定で有効になりませんが、特定のユーザー入力コントロールに対しては選択的に有効になります。 これは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のジャーナリングの実装を含む、ジャーナリング サービスによって読み取られるプロパティです。通常は、複数のナビゲーション ステップにわたって永続化する必要があるユーザー コントロール (一覧におけるユーザー選択など) に設定します。 ジャーナリングの詳細については、「[ナビゲーションの概要](../app-development/navigation-overview.md)」を参照してください。  
  
<a name="Reading_FrameworkPropertyMetadata"></a>
## <a name="reading-frameworkpropertymetadata"></a>FrameworkPropertyMetadata の読み取り  
 上でリンクされている各プロパティは、<xref:System.Windows.FrameworkPropertyMetadata> によって直接の基底クラス <xref:System.Windows.UIPropertyMetadata> に追加される特定のプロパティです。 これらのプロパティの既定値はいずれも `false` です。 これらのプロパティの値を知るためにメタデータを要求する場合は、返されたメタデータを <xref:System.Windows.FrameworkPropertyMetadata> にキャストしてから、必要に応じて個々のプロパティの値を確認する必要があります。  
  
<a name="Specifying_Metadata"></a>
## <a name="specifying-metadata"></a>メタデータの指定  
 新しい依存関係プロパティの登録にメタデータを適用する目的で、メタデータ インスタンスを新しく作成するときは、基底の <xref:System.Windows.PropertyMetadata> を使用するか、<xref:System.Windows.FrameworkPropertyMetadata> などの派生クラスを使用するかを選択できます。 通常は <xref:System.Windows.FrameworkPropertyMetadata> を使用します。特に、プロパティがプロパティ システムと対話する場合や、レイアウトやデータ バインディングなどの [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 機能と対話する場合はこのクラスを使用します。 より高度なシナリオでは、<xref:System.Windows.FrameworkPropertyMetadata> から派生して独自のメタデータ報告クラスを作成し、メンバーに追加情報が含まれるようにします。 <xref:System.Windows.PropertyMetadata> または <xref:System.Windows.UIPropertyMetadata> を使用して、実装の機能をサポートする度合いを通知することもできます。  
  
 既存のプロパティ (<xref:System.Windows.DependencyProperty.AddOwner%2A> または <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> の呼び出し) については、常に元の登録で使用されているメタデータ型によりオーバーライドする必要があります。  
  
 <xref:System.Windows.FrameworkPropertyMetadata> のインスタンスを作成する場合、フレームワーク プロパティの特性を通知する特定のプロパティの値をそのメタデータに読み込むには、次の 2 つの方法があります。  
  
1. `flags` パラメーターを使用可能な <xref:System.Windows.FrameworkPropertyMetadata> コンストラクター シグネチャを使用します。 このパラメーターには、<xref:System.Windows.FrameworkPropertyMetadataOptions> 列挙フラグの結合された該当する値をすべて指定します。  
  
2. `flags` パラメーターを持たないシグネチャのいずれかを使用し、各特性の任意の変更について、<xref:System.Windows.FrameworkPropertyMetadata> 上の各報告ブール型プロパティを `true` に設定します。 この場合、この依存関係プロパティを持つすべての要素の構築前に、これらのプロパティを設定する必要があります。`flags` パラメーターを使用せずに引き続きメタデータを読み込めるよう、これらのブール型プロパティは読み書き可能な状態ですが、プロパティの使用前にメタデータを事実上シールする必要があります。 そのため、メタデータの要求後にこれらのプロパティを設定しようとすると、無効な操作となります。  
  
<a name="Framework_Property_Metadata_Merge_Behavior"></a>
## <a name="framework-property-metadata-merge-behavior"></a>フレームワーク プロパティ メタデータのマージ動作  
 フレームワーク プロパティ メタデータをオーバーライドすると、さまざまなメタデータ特性がマージされるか置き換えられます。  
  
- <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> はマージされます。 新しい <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> を追加すると、そのコールバックがメタデータに格納されます。 オーバーライドで <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> を指定しないと、<xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> の値は、それをメタデータで指定した最も近い先祖からの参照としてレベル上げされます。  
  
- <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> の実際のプロパティ システム動作では、階層内のすべてのメタデータ所有者用の実装が維持されてテーブルに追加されます。プロパティ システムによる実行順序としては、最派生クラスのコールバックが最初に呼び出されます。 継承されたコールバックは、それらをメタデータに配置したクラスによって所有されていると見なされ、それぞれ 1 回だけ実行されます。  
  
- <xref:System.Windows.PropertyMetadata.DefaultValue%2A> は置き換えられます。 オーバーライドで <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> を指定しないと、<xref:System.Windows.PropertyMetadata.DefaultValue%2A> の値は、それをメタデータで指定した最も近い先祖のものになります。  
  
- <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> の実装は置き換えられます。 新しい <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> を追加すると、そのコールバックがメタデータに格納されます。 オーバーライドで <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> を指定しないと、<xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> の値は、それをメタデータで指定した最も近い先祖からの参照としてレベル上げされます。  
  
- プロパティ システム動作では、直接のメタデータ内の <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> だけが呼び出されます。 階層内の他の <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> の実装への参照が保持されることはありません。  
  
- <xref:System.Windows.FrameworkPropertyMetadataOptions> 列挙型のフラグは、ビットごとの OR 演算として組み合わされます。  <xref:System.Windows.FrameworkPropertyMetadataOptions> を指定しても、元のオプションは上書きされません。  オプションを変更するには、<xref:System.Windows.FrameworkPropertyMetadata> で対応するプロパティを設定します。 たとえば、元の <xref:System.Windows.FrameworkPropertyMetadata> オブジェクトで <xref:System.Windows.FrameworkPropertyMetadataOptions.NotDataBindable?displayProperty=nameWithType> フラグが設定されている場合は、<xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A?displayProperty=nameWithType> を `false` に設定することでこのフラグを変更できます。  
  
 この動作は <xref:System.Windows.FrameworkPropertyMetadata.Merge%2A> によって実装され、派生メタデータ クラスでオーバーライドできます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.DependencyProperty.GetMetadata%2A>
- [依存関係プロパティのメタデータ](dependency-property-metadata.md)
- [依存関係プロパティの概要](dependency-properties-overview.md)
- [カスタム依存関係プロパティ](custom-dependency-properties.md)
