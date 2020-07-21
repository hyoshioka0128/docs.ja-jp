---
title: アプリケーション パフォーマンスの計画
ms.date: 03/30/2017
helpviewer_keywords:
- applications [WPF], optimizing
- WPF application [WPF], optimizing
ms.assetid: c91bd0c5-a193-46ff-9da1-eb7a3a76a3b3
ms.openlocfilehash: 70dda68112d47d3e5a0609a5df7696920477c698
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62032865"
---
# <a name="planning-for-application-performance"></a>アプリケーション パフォーマンスの計画
パフォーマンスの目標達成が成功するかどうかは、パフォーマンス戦略をどの程度適切に展開させるかによって決まります。 計画は、製品の開発における最初の段階です。 このトピックでは、優れたパフォーマンス戦略を立てるための非常にシンプルな規則をいくつか説明します。  
  
## <a name="think-in-terms-of-scenarios"></a>シナリオの観点から考える  
 シナリオは、アプリケーションの重要なコンポーネントに集中するのに役立ちます。 シナリオは一般的に、競合製品だけでなく、顧客からも派生します。 常に顧客を調査し、自社製品、および競合他社の製品に本当に夢中にさせるものを見つけます。 顧客のフィードバックは、アプリケーションの主要なシナリオを特定するのに役立ちます。 たとえば、起動時に使用されるコンポーネントを設計する場合、アプリケーションの起動時に、コンポーネントは 1 回だけ呼び出される可能性があります。 起動時間が主要なシナリオとなります。 主要なシナリオのその他の例としては、アニメーション シーケンスに必要なフレーム レートや、アプリケーションで許容される最大ワーキング セットなどがあります。  
  
## <a name="define-goals"></a>目標を定義する  
 目標は、アプリケーションがより高速にあるいはより低速に実行されているかを判断するのに役立ちます。 すべてのシナリオに対して目標を定義する必要があります。 定義するすべてのパフォーマンス目標は、お客様の期待に基づいている必要があります。 まだ解決されていない問題が多くあると、アプリケーション開発サイクルの早い段階でパフォーマンス目標を設定することが難しくなる場合があります。 しかし、目標をまったく持たないより、初期目標を設定し、それを後で見直す方が得策です。  
  
## <a name="understand-your-platform"></a>プラットフォームについて理解する  
 アプリケーションの開発サイクル中に、測定、調査、調整または修正のサイクルを常に維持します。 開発サイクルの最初から最後まで、信頼性の高い安定した環境で、アプリケーションのパフォーマンスを測定する必要があります。 外部要因による変動を避ける必要があります。 たとえば、パフォーマンスをテストする場合に、パフォーマンス テストの結果に影響しないように、ウイルス対策、または SMS などの自動更新を無効にする必要があります。 アプリケーションのパフォーマンスを測定したら、最大の改善となる変更を特定する必要があります。 アプリケーションを変更したら、再度サイクルを開始します。  
  
## <a name="make-performance-tuning-an-iterative-process"></a>反復的なプロセスのパフォーマンス チューニングを行う  
 使用する各機能の相対コストを把握しておく必要があります。 たとえば、Microsoft .NET Framework でリフレクションを使用すると、一般的に、コンピューティング リソースの観点からパフォーマンスに負担がかかるため、慎重に使用する必要があります。 これは、単にアプリケーションのパフォーマンス要件と、使用する機能のパフォーマンス要求とのバランスを慎重に取る必要があるという意味であり、リフレクションの使用を避けることを意味するものではありません。  
  
## <a name="build-towards-graphical-richness"></a>グラフィックを豊かなものにするために構築する  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションのパフォーマンスの実現に向けてスケーラブルなアプローチを生み出すための主な手法は、グラフィックを豊かで複雑なものにするために構築することです。 シナリオの目標を達成するには常に、パフォーマンスへの負担が最も小さいリソースをまず使用します。 これらの目標を達成したら、パフォーマンスへの負担がより大きい機能を使用し、常にシナリオの目標を念頭に置いて、グラフィックを豊かなものにするために構築します。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は非常に豊かなプラットフォームであり、非常に豊かなグラフィック機能を備えていることを覚えておいてください。 何も考えずにパフォーマンスへの負担が大きい機能を使用すると、アプリケーション全体のパフォーマンスに悪影響を及ぼす可能性があります。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールは、そのコントロールの動作を変更することなく、外観を広範にカスタマイズできるようにすることで、本質的に拡張可能です。 スタイル、データ テンプレート、コントロール テンプレートを活用することで、パフォーマンスの要件に合わせてカスタマイズ可能な[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] を作成し、段階的に進化させることができます。  
  
## <a name="see-also"></a>関連項目

- [WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)
- [ハードウェアの活用](optimizing-performance-taking-advantage-of-hardware.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
- [2D グラフィックスとイメージング](optimizing-performance-2d-graphics-and-imaging.md)
- [オブジェクトの動作](optimizing-performance-object-behavior.md)
- [アプリケーション リソース](optimizing-performance-application-resources.md)
- [[テキスト]](optimizing-performance-text.md)
- [データ バインディング](optimizing-performance-data-binding.md)
- [パフォーマンスに関するその他の推奨事項](optimizing-performance-other-recommendations.md)
