---
title: グラフィックス サービスの 3 つのカテゴリ
ms.date: 03/30/2017
helpviewer_keywords:
- imaging
- graphics [Windows Forms], categories
- 2D vector graphics
- vector graphics
- typography
ms.assetid: 068c0ef3-f6ee-4d58-a7b6-eb2531ead408
ms.openlocfilehash: fa7391ef0f7170ddb9d9d24aa5a1a03635bf46e0
ms.sourcegitcommit: e48a54ebe62e874500a7043f6ee0b77a744d55b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80291723"
---
# <a name="three-categories-of-graphics-services"></a>グラフィックス サービスの 3 つのカテゴリ
Windows フォームのグラフィックス製品は、次の 3 つの大きなカテゴリに分類されます。  
  
- 2 次元 (2 次元) ベクトル グラフィックス  
  
- イメージング  
  
- タイポグラフィ  
  
## <a name="2d-vector-graphics"></a>2D ベクトル グラフィックス  
 直線、曲線、図などの 2 次元ベクトル グラフィックスは、座標系上のポイントのセットによって指定されるプリミティブです。 たとえば、直線は 2 つの端点で指定され、四角形は左上隅の位置を示す点と、幅と高さを示す数値のペアで指定されます。 単純パスは、直線で接続されたポイントの配列で指定されます。 ベジェ スプラインは、4 つのコントロール ポイントで指定された高度な曲線です。  
  
 GDI+ には、プリミティブ自体に関する情報、プリミティブの描画方法に関する情報を格納するクラス、および実際に描画を行うクラスを格納するクラスと構造体が用意されています。 たとえば、この構造体<xref:System.Drawing.Rectangle>には、四角形の位置とサイズが格納されます。この<xref:System.Drawing.Pen>クラスには、線の色、線の幅、線のスタイルに関する情報が格納されます。<xref:System.Drawing.Graphics>クラスには、線、長方形、パス、およびその他の図形を描画するためのメソッドがあります。 閉じた図形や<xref:System.Drawing.Brush>パスが色やパターンで塗りつぶされる方法に関する情報を格納するクラスもいくつかあります。  
  
 グラフィック コマンドのシーケンスであるベクター イメージをメタファイルに記録できます。 GDI+ は<xref:System.Drawing.Imaging.Metafile>、メタファイルの記録、表示、保存のためのクラスを提供します。 <xref:System.Drawing.Imaging.MetafileHeader>クラスと<xref:System.Drawing.Imaging.MetaHeader>クラスを使用すると、メタファイル ヘッダーに格納されているデータを検査できます。  
  
## <a name="imaging"></a>イメージング  
 特定の種類の画像は、ベクトルグラフィックスのテクニックでは表示が困難または不可能です。 たとえば、ツール バー ボタン上の図やアイコンとして表示される図は、線や曲線のコレクションとして指定するのが困難です。 混雑した野球場の高解像度デジタル写真は、ベクトル技術で作成することはさらに困難です。 このタイプのイメージはビットマップとして保存され、画面上の個々のドットの色を表す数値の配列です。 GDI+ は<xref:System.Drawing.Bitmap>、ビットマップの表示、操作、および保存を行うためのクラスを提供します。  
  
## <a name="typography"></a>タイポグラフィ  
 文字体裁は、さまざまなフォント、サイズ、およびスタイルでテキストを表示します。 GDI+ は、この複雑なタスクを広範囲にサポートします。 GDI+ の新機能の 1 つはサブピクセル アンチエイリアシングで、LCD 画面に表示されるテキストの外観が滑らかになります。  
  
 さらに、Windows フォームには、GDI 機能を持つテキストをそのクラス<xref:System.Windows.Forms.TextRenderer>で描画するオプションが用意されています。  
  
## <a name="see-also"></a>関連項目

- [グラフィックスの概要](graphics-overview-windows-forms.md)
- [GDI+ マネージド コードについて](about-gdi-managed-code.md)
- [マネージド グラフィックス クラスの使用](using-managed-graphics-classes.md)
