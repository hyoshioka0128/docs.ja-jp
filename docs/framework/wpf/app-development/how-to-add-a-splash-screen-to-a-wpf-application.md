---
title: スプラッシュ スクリーンを追加する方法
description: Windows Presentation Foundation (WPF) アプリケーションにスタートアップ ウィンドウまたはスプラッシュ スクリーンを追加する方法について説明します。
ms.date: 08/18/2018
helpviewer_keywords:
- WPF [WPF], splash screen
- startup window [WPF]
- SplashScreen class [WPF]
- splash screen [WPF]
ms.assetid: d70a25c4-5fb9-4c27-b01d-b1b8ef39b3fd
ms.openlocfilehash: 0d0cf2e2a550320650c3b4a0c257071a0403c32b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617961"
---
# <a name="how-to-add-a-splash-screen-to-a-wpf-application"></a>方法: スプラッシュ スクリーンを WPF アプリケーションに追加する

このトピックでは、Windows Presentation Foundation (WPF) アプリケーションにスタートアップ ウィンドウ ("*スプラッシュ スクリーン*") を追加する方法について説明します。

## <a name="to-add-an-existing-image-as-a-splash-screen"></a>既存の画像をスプラッシュ スクリーンとして追加するには

1. スプラッシュ スクリーンとして使用する画像を作成または検索します。 Windows Imaging Component (WIC) でサポートされている任意の画像形式を使用できます。 たとえば、BMP、GIF、JPEG、PNG、または TIFF 形式を使用できます。

2. WPF アプリケーション プロジェクトに画像ファイルを追加します。

3. **ソリューション エクスプローラー**で、画像を選択します。

4. プロパティ ウィンドウで、 **[ビルド アクション]** プロパティのドロップダウン矢印をクリックします。

5. ドロップダウン リストから **[スプラッシュスクリーン]** を選択します。

6. **F5** キーを押してアプリケーションをビルドし、実行します。

     スプラッシュ スクリーンの画像が画面の中央に表示された後、メイン アプリケーション ウィンドウが表示されると消えます。

## <a name="to-exclude-the-splash-screen-from-build"></a>ビルドからスプラッシュ スクリーンを除外するには

1. **ソリューション エクスプローラー**で、スプラッシュ スクリーンの画像を選択します。

2. **[プロパティ]** ウィンドウで、 **[ビルド アクション]** を **[なし]** に設定します。

## <a name="to-remove-the-splash-screen-from-an-application"></a>アプリケーションからスプラッシュ スクリーンを削除するには

**ソリューション エクスプローラー**で、スプラッシュ スクリーンの画像を削除します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.SplashScreen>
- [方法: 既存の項目をプロジェクトに追加する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/9f4t9t92(v=vs.100))
