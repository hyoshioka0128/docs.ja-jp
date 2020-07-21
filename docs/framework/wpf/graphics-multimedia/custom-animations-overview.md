---
title: カスタム アニメーションの概要
ms.date: 03/30/2017
helpviewer_keywords:
- custom classes [WPF], animation
- key frames [WPF], custom
- custom key frames [WPF]
- animation [WPF], custom classes
- custom animation classes [WPF]
ms.assetid: 9be69d50-3384-4938-886f-08ce00e4a7a6
ms.openlocfilehash: c5f315992e8ae37bc79602e6986d90e7af591fb2
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186550"
---
# <a name="custom-animations-overview"></a>カスタム アニメーションの概要
このトピックでは、カスタム キー フレームやアニメーション クラスを作成して、またはフレームごとのコールバックを使ってバイパスすることにより、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のアニメーション システムを拡張する方法と、それが必要な状況について説明します。  
  
<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によって提供されるさまざまな種類のアニメーションに精通している必要があります。 詳しくは、「From/To/By アニメーションの概要」、「[キー フレーム アニメーションの概要](key-frame-animations-overview.md)」、および「[パス アニメーションの概要](path-animations-overview.md)」をご覧ください。  
  
 アニメーションのクラスは <xref:System.Windows.Freezable> クラスを継承するため、<xref:System.Windows.Freezable> オブジェクトと、<xref:System.Windows.Freezable> からの継承方法について、理解している必要があります。 詳しくは、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。  
  
<a name="extendingtheanimationsystem"></a>
## <a name="extending-the-animation-system"></a>アニメーション システムの拡張  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のアニメーション システムには、使う組み込み機能のレベルに応じて、さまざまな拡張方法があります。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のアニメーション エンジンには、次の 3 つの主な機能拡張ポイントがあります。  
  
- *\<Type>* KeyFrame クラス (<xref:System.Windows.Media.Animation.DoubleKeyFrame> など) の 1 つから継承することにより、カスタム キー フレーム オブジェクトを作成します。 この方法では、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーション エンジンの組み込み機能のほとんどを使います。  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline> または *\<Type>* AnimationBase クラスの 1 つから継承することにより、独自のアニメーション クラスを作成します。  
  
- フレームごとのコールバックを使って、フレームごとにアニメーションを生成します。 この方法は、アニメーションおよびタイミング システムを完全にバイパスします。  
  
 次の表では、いくつかのアニメーション システム拡張シナリオについて説明します。  
  
|目的...|使う方法|  
|-------------------------|-----------------------|  
|対応する *\<Type>* AnimationUsingKeyFrames がある型の値の間の補間をカスタマイズする|カスタム キー フレームを作成します。 詳しくは、「[カスタム キー フレームを作成する](#createacustomkeyframe)」セクションをご覧ください。|  
|対応する *\<Type>* Animation がある型の値の間の補間以外の部分もカスタマイズする|アニメーション化する型に対応する *\<Type>* AnimationBase クラスを継承するカスタム アニメーション クラスを作成します。 詳しくは、「[カスタム アニメーション クラスを作成する](#createacustomanimationtype)」セクションをご覧ください。|  
|対応する [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーションがない型をアニメーション化する|<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> を使用するか、または <xref:System.Windows.Media.Animation.AnimationTimeline> を継承するクラスを作成します。 詳しくは、「[カスタム アニメーション クラスを作成する](#createacustomanimationtype)」セクションをご覧ください。|  
|フレームごとに計算され、最後のオブジェクト相互作用セットに基づく値のある、複数のオブジェクトをアニメーション化する|フレームごとのコールバックを使います。 詳しくは、「[フレームごとのコールバックを使用する](#useperframecallback)」セクションをご覧ください。|  
  
<a name="createacustomkeyframe"></a>
## <a name="create-a-custom-key-frame"></a>カスタム キー フレームを作成する  
 カスタム キー フレーム クラスの作成は、アニメーション システムを拡張する最も簡単な方法です。 キー フレーム アニメーションに対して異なる補間方法が必要なときは、このアプローチを使います。  「[キー フレーム アニメーションの概要](key-frame-animations-overview.md)」で説明されているように、キー フレーム アニメーションはキー フレーム オブジェクトを使って出力値を生成します。 各キー フレーム オブジェクトは 3 つの機能を実行します。  
  
- <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> プロパティを使用してターゲット値を指定します。  
  
- <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A> プロパティを使用して、その値に到達する必要がある時間を指定します。  
  
- InterpolateValueCore メソッドを実装することで、前のキー フレームの値とそれ自体の値の間を補間します。  
  
 **実装の説明**  
  
 *\<Type>* KeyFrame 抽象クラスから派生して、InterpolateValueCore メソッドを実装します。 InterpolateValueCore メソッドは、キー フレームの現在の値を返します。 2 つのパラメーターとして、前のキー フレームの値と、0 から 1 の範囲の進行状況の値を受け取ります。 進行状況 0 はキー フレームが開始したばかりであることを示し、値 1 はキー フレームが完了したばかりで、<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A> プロパティによって指定されている値を返す必要があることを示します。  
  
 *\<Type>* KeyFrame クラスは <xref:System.Windows.Freezable> クラスを継承するため、独自クラスの新しいインスタンスを返すように、<xref:System.Windows.Freezable.CreateInstanceCore%2A> コアもオーバーライドする必要があります。 クラスが依存関係プロパティを使ってデータを保存しない場合、または作成の後で追加の初期化が必要な場合は、他のメソッドのオーバーライドが必要な場合があります。詳しくは、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。  
  
 カスタム *\<Type>* KeyFrame アニメーションを作成した後は、その型の *\<Type>* AnimationUsingKeyFrames でそれを使うことができます。  
  
<a name="createacustomanimationtype"></a>
## <a name="create-a-custom-animation-class"></a>カスタム アニメーション クラスを作成する  
 独自のアニメーション型を作成すると、オブジェクトをアニメーション化する方法をいっそう細かく制御できます。 独自のアニメーション型を作成するには、2 つの推奨される方法があります。<xref:System.Windows.Media.Animation.AnimationTimeline> クラスから派生する方法と、 *\<Type>* AnimationBase クラスから派生する方法です。 *\<Type>* Animation クラスまたは *\<Type>* AnimationUsingKeyFrames クラスからの派生は推奨されません。  
  
### <a name="derive-from-typeanimationbase"></a>\<Type>AnimationBase から派生する  
 *\<Type>* AnimationBase クラスからの派生は、新しいアニメーション型を作成する最も簡単な方法です。 対応する *\<Type>* AnimationBase クラスが既にある型の新しいアニメーションを作成する場合は、この方法を使います。  
  
 **実装の説明**  
  
 *\<Type>* Animation から派生して、GetCurrentValueCore メソッドを実装します。 GetCurrentValueCore メソッドは、アニメーションの現在の値を返します。 これは、3 つのパラメーターとして、推奨される開始値、推奨される終了値、およびアニメーションの進行状況を特定するために使用する <xref:System.Windows.Media.Animation.AnimationClock> を受け取ります。  
  
 *\<Type>* AnimationBase クラスは <xref:System.Windows.Freezable> クラスを継承するため、独自クラスの新しいインスタンスを返すように、<xref:System.Windows.Freezable.CreateInstanceCore%2A> コアもオーバーライドする必要があります。 クラスが依存関係プロパティを使ってデータを保存しない場合、または作成の後で追加の初期化が必要な場合は、他のメソッドのオーバーライドが必要な場合があります。詳しくは、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。  
  
 詳しくは、アニメーション化する型の *\<Type>* AnimationBase クラスの GetCurrentValueCore メソッドのドキュメントをご覧ください。 例については、「[Custom Animation Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/CustomAnimation)」(カスタム アニメーションのサンプル) をご覧ください。  
  
 **別の方法**  
  
 アニメーション値を補間する方法を変更したいだけの場合は、いずれかの *\<Type>* KeyFrame クラスからの派生を検討します。 作成したキー フレームを、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によって提供される対応する *\<Type>* AnimationUsingKeyFrames で使うことができます。  
  
### <a name="derive-from-animationtimeline"></a>AnimationTimeline から派生する  
 一致する [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーションがまだ存在しない型のアニメーションを作成する場合、または厳密に型指定されていないアニメーションを作成したい場合は、<xref:System.Windows.Media.Animation.AnimationTimeline> クラスから派生します。  
  
 **実装の説明**  
  
 <xref:System.Windows.Media.Animation.AnimationTimeline> クラスから派生して、次のメンバーをオーバーライドします。  
  
- <xref:System.Windows.Freezable.CreateInstanceCore%2A> – 新しいクラスが具象の場合、クラスの新しいインスタンスを返すように <xref:System.Windows.Freezable.CreateInstanceCore%2A> をオーバーライドする必要があります。  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> – アニメーションの現在の値を返すように、このメソッドをオーバーライドします。 既定の開始値、既定の終了値、<xref:System.Windows.Media.Animation.AnimationClock> の、3 つのパラメーターを受け取ります。 アニメーションの現在の時間または進行状況を取得するには、<xref:System.Windows.Media.Animation.AnimationClock> を使用します。 既定の開始値と終了値を使うかどうかを選択できます。  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline.IsDestinationDefault%2A> – <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> メソッドによって指定された既定の終了値をアニメーションで使用するかどうかを示すために、このプロパティをオーバーライドします。  
  
- <xref:System.Windows.Media.Animation.AnimationTimeline.TargetPropertyType%2A> – アニメーションが生成する出力の <xref:System.Type> を示すように、このプロパティをオーバーライドします。  
  
 クラスが依存関係プロパティを使ってデータを保存しない場合、または作成の後で追加の初期化が必要な場合は、他のメソッドのオーバーライドが必要な場合があります。詳しくは、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。  
  
 推奨される ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーションによって使われる) パラダイムは、2 つの継承レベルを使うことです。  
  
1. <xref:System.Windows.Media.Animation.AnimationTimeline> から派生する抽象 *\<Type>* AnimationBase クラスを作成します。 このクラスでは、<xref:System.Windows.Media.Animation.AnimationTimeline.TargetPropertyType%2A> メソッドをオーバーライドする必要があります。 また、新しい抽象メソッド GetCurrentValueCore を導入し、既定の開始値と終了値パラメーターの型を検証してから GetCurrentValueCore を呼び出すように <xref:System.Windows.Media.Animation.AnimationTimeline.GetCurrentValue%2A> をオーバーライドする必要があります。  
  
2. 新しい *\<Type>* AnimationBase クラスから継承し、<xref:System.Windows.Freezable.CreateInstanceCore%2A> メソッド、導入した GetCurrentValueCore メソッド、<xref:System.Windows.Media.Animation.AnimationTimeline.IsDestinationDefault%2A> プロパティをオーバーライドする、別のクラスを作成します。  
  
 **別の方法**  
  
 対応する From/To/By アニメーションまたはキー フレーム アニメーションがない型をアニメーション化する場合は、<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> の使用を検討します。 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>は弱く型指定されているため、任意の型の値をアニメーション化できます。 この方法の欠点は、<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> が離散補間のみをサポートすることです。  
  
<a name="useperframecallback"></a>
## <a name="use-per-frame-callback"></a>フレームごとのコールバックを使用する  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アニメーション システムを完全にバイパスする必要があるときは、この方法を使います。 この方法の 1 つのシナリオは、各アニメーション ステップでオブジェクトの最後の一連のやり取りに基づいてアニメーション化されるオブジェクトの新しい向きまたは位置を再計算する必要がある物理アニメーションです。  
  
 **実装の説明**  
  
 この概要で説明されている他の方法とは異なり、フレームごとのコールバックを使うために、カスタム アニメーション クラスまたはカスタム キー フレーム クラスを作成する必要はありません。  
  
 代わりに、アニメーション化するオブジェクトを格納しているオブジェクトの <xref:System.Windows.Media.CompositionTarget.Rendering> イベントに登録します。 このイベント ハンドラー メソッドは、フレームごとに 1 回呼び出されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] がビジュアル ツリーの永続化されたレンダリング データを構成ツリーにマーシャリングするたびに、イベント ハンドラー メソッドが呼び出されます。  
  
 イベント ハンドラーでは、アニメーション効果に必要なあらゆる計算を実行し、これらの値を使用してアニメーション化するオブジェクトのプロパティを設定します。  
  
 現在のフレームの表現時間を取得するために、このイベントに関連付けられている <xref:System.EventArgs> を、<xref:System.Windows.Media.RenderingEventArgs> としてキャストできます。これにより、現在のフレームのレンダリング時間を取得するために使用できる <xref:System.Windows.Media.RenderingEventArgs.RenderingTime%2A> プロパティが提供されます。  
  
 詳細については、「<xref:System.Windows.Media.CompositionTarget.Rendering>」ページを参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Animation.AnimationTimeline>
- <xref:System.Windows.Media.Animation.IKeyFrame>
- [プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)
- [Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)
- [キー フレーム アニメーションの概要](key-frame-animations-overview.md)
- [パス アニメーションの概要](path-animations-overview.md)
- [アニメーションの概要](animation-overview.md)
- [アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)
- [カスタム アニメーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Animation/CustomAnimation)
