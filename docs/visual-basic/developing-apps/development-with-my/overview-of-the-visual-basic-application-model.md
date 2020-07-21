---
title: Visual Basic アプリケーション モデルの概要
ms.date: 07/20/2015
helpviewer_keywords:
- My.Application object [Visual Basic], Visual Basic application model
- Visual Basic application model
ms.assetid: 17538984-84fe-43c9-82c8-724c9529fe8b
ms.openlocfilehash: 46177d0af7e5df767eb8421caf424880baac615e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411728"
---
# <a name="overview-of-the-visual-basic-application-model"></a>Visual Basic アプリケーション モデルの概要

Visual Basic は、Windows フォーム アプリケーションの動作を制御するための正しく定義されたモデル (Visual Basic アプリケーション モデル) を提供します。 このモデルには、アプリケーションのスタートアップとシャットダウンを処理するためのイベントと、ハンドルされない例外をキャッチするためのイベントが含まれます。 さらに、単一インスタンス アプリケーションを開発するためのサポートも提供します。 このアプリケーション モデルは拡張可能であるため、より多くのコントロールを必要とする開発者は、オーバーライド可能なメソッドをカスタマイズできます。  
  
## <a name="uses-for-the-application-model"></a>アプリケーション モデルの使用  

 一般的なアプリケーションは、スタートアップ時とシャットダウン時にタスクを実行する必要があります。 たとえば、そのスタートアップ時には、スプラッシュ スクリーンの表示、データベース接続の確立、保存された状態の読み込みなどが行われます。 また、アプリケーションのシャットダウン時には、データベース接続が閉じられたり、現在の状態が保存されたりします。 さらに、ハンドルされない例外などのために予期せずシャットダウンした場合、アプリケーションにより特定のコードが実行されます。  
  
 Visual Basic アプリケーション モデルを使用すると、"*単一インスタンス*" アプリケーションを簡単に作成できます。 単一インスタンス アプリケーションは、一度に実行できるアプリケーションのインスタンスが 1 つのみであるという点で、通常のアプリケーションとは異なります。 単一インスタンス アプリケーションの別のインスタンスを起動しようとすると、`StartupNextInstance` イベントを使用して、別の起動が試行されたことが元のインスタンスに通知されます。 通知には、後続のインスタンスのコマンドライン引数が含まれます。 この後、アプリケーションの後続のインスタンスは、初期化が発生する前に閉じられます。  
  
 単一インスタンス アプリケーションは、起動されると、それがアプリケーションの最初のインスタンスであるか、または後続のインスタンスであるかを確認します。  
  
- 最初のインスタンスである場合、通常どおり起動されます。  
  
- 最初のインスタンスの実行中にアプリケーションを起動しようとするたびに、後続の試行ではまったく異なる動作が発生します。 後続の試行は、最初のインスタンスにコマンドライン引数が通知された後、即座に終了します。 最初のインスタンスは、`StartupNextInstance` イベントを処理して、後続のインスタンスのコマンドライン引数を判別して、実行を継続します。  
  
     次の図は、後続のインスタンスが最初のインスタンスに通知する方法を示しています。  
  
     ![単一インスタンス アプリケーションのイメージを示す図。](./media/overview-of-the-visual-basic-application-model/single-instance-application.gif)  
  
 `StartupNextInstance` イベントを処理することにより、単一インスタンス アプリケーションの動作を制御することができます。 たとえば、Microsoft Outlook は、通常、単一インスタンス アプリケーションとして実行されます。Outlook の実行中に、Outlook を再度起動しようとすると、フォーカスは元のインスタンスに移りますが、別のインスタンスは開かれません。  
  
## <a name="events-in-the-application-model"></a>アプリケーション モデル内のイベント  

 アプリケーション モデルには、次のイベントが含まれます。  
  
- **アプリケーションのスタートアップ**: アプリケーションは、起動時に、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> イベントを発生させます。 このイベントを処理することにより、メイン フォームが読み込まれる前にアプリケーションを初期化するコードを追加できます。 `Startup` イベントは、必要に応じて、スタートアップ プロセスのそのフェーズ中にアプリケーションの実行をキャンセルするためにも提供されます。  
  
     アプリケーションのスタートアップ コードの実行中にスプラッシュ スクリーンを表示するようにアプリケーションを構成できます。 アプリケーション モデルでは、既定により、`/nosplash` または `-nosplash` のいずれかのコマンドライン引数が使用されている場合、スプラッシュ スクリーンを表示しません。  
  
- **単一インスタンス アプリケーション**: 単一インスタンス アプリケーションの後続のインスタンスが開始されると、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> イベントが発生します。 このイベントは、後続のインスタンスのコマンドライン引数を渡します。  
  
- **ハンドルされない例外**: アプリケーションは、ハンドルされない例外を検出すると、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> イベントを発生させます。 そのイベントのハンドラーは、例外を調べて、実行を継続するかどうかを判断できます。  
  
     `UnhandledException` イベントは、場合によっては発生しないことがあります。 詳細については、「<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>」を参照してください。  
  
- **ネットワーク接続の変更**: コンピューターのネットワークの可用性が変更されると、アプリケーションは <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged> イベントを発生させます。  
  
     `NetworkAvailabilityChanged` イベントは、場合によっては発生しないことがあります。 詳細については、「<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>」を参照してください。  
  
- **アプリケーションのシャットダウン**: アプリケーションは、シャットダウンしようとしていることを通知する <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> イベントを提供します。 そのイベント ハンドラーでは、アプリケーションが実行する必要がある操作 (たとえば、終了と保存など) が完了していることを確認できます。 アプリケーションを、メイン フォールが閉じられたときにシャットダウンするように構成することも、すべてのフォームが閉じられたときにのみシャットダウンするように構成することもできます。  
  
## <a name="availability"></a>可用性  

 既定では、Visual Basic アプリケーション モデルは、Windows フォーム プロジェクトで使用できます。 別のスタートアップ オブジェクトを使用するようにアプリケーションを構成する場合、またはカスタムの `Sub Main` を使用してアプリケーション コードを開始する場合、このアプリケーション モデルを使用するために、そのオブジェクトまたはクラスで <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> クラスの実装を提供する必要があります。 スタートアップ オブジェクトの変更については、「[アプリケーション ページ、プロジェクト デザイナー (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>
- <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>
- [Visual Basic アプリケーション モデルの拡張](../customizing-extending-my/extending-the-visual-basic-application-model.md)
